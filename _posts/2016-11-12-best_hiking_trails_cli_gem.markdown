---
layout: post
title:  "Best Hiking Trails CLI Gem"
date:   2016-11-12 22:20:24 +0000
---


I decided to create a hiking trail CLI gem that would post the top 10 hikes and allow the user to get information about each hike. I think what took me the longest was figuring out what kind of gem I would like to build. Once I was able to come up with a subject (this took me about 4 hours) everything seemed to flow nicely from then on.

## The challenge
Finding a good website to scrape was definitely a challenge because most of the websites that I tried to scrape had very unsemantic HTML. For instance the original website I was trying to scrape information about each hiking trail had everything nested inside of a p tag for instance: 

`<p>`<br>
`Location:`<br>
`<br>`<br>
`Distance:`<br>
`<br>`<br>
`Country:`<br>
`<br>`<br>
`Information:`<br>
`<br>`<br>
`</p>`<br>

Eventually I was able to find a website that I thought was good enough to scrape. The website I used also has very unsemantic HTML so I knew scraping this data was going to be a challenge.

### The Trail Titles

I noticed every one of the trail titles were in H3 tags.When I used Nokogiri's search method and targeted the H3's I would end up receiving a bunch of unwanted information that wasn't just the hiking trail titles I wanted. To combat this I was able to use Nokogiri's xpath method which grabs all elements that you want to target which would look something like:

`<h3>Title1</h3>`<br>
`<h3>Title2</h3>`<br>
`<h3>Title3</h3>`<br>

After I received the all of the H3 elements on the page I looped through each one of the H3 elements and used Nokogiri's .content method to pull the content out of each element. Here is the code:

` def self.scrape_best_trails`<br>
    `trail_obj = []`<br>
    `doc = Nokogiri::HTML(open("https://www.theoutbound.com/theoutbound/the-best-25-hikes-in-america"))`<br>
    `trails = doc.xpath("//h3").each_with_index do |name, i|` **---Loop through each title**<br>
      `trail = self.new`   **--Create a new object for each title**<br>
     ` trail.name = name.content` **--Set the name of each object**<br>
     ` trail.information = self.scrape_information(i)` **--Set the information of each object and used i as my method argument ( look below )**<br>
     ` trail_obj << trail`<br>
     ` break if i == 9;` --Break after creating 10 objects<br>
   ` end`<br>
    `trail_obj`<br>
  `end`<br>
	
### The Trail Information

Getting the information was a little more tricky. Every trail information was in P tags along with pretty much everything else on the page. Originally each trail had its own page with information about each trail, so what I did was scrape each one of these pages (there was 10 pages) but I realized this was way too slow and too much data to grab. I ended up just grabbing every P in the content section of the first page which contained author names and useless information that I didn't want. To combat this I looped through each one of the p tags and used gsub to take out the useless information that I didn't want. Here is the code:

  `def self.scrape_information(number)` **--Created a method that took 1 argument which I used my loop above to associate each information with each one of my titles**<br>
    `information_arr = []`<br>
    `doc = Nokogiri::HTML(open("https://www.theoutbound.com/theoutbound/the-best-25-hikes-in-america"))`<br>
    `trails = doc.search(".description.story-content p").each_with_index do |name, i|` **-- Loop through each one of my P tags inside of the main content section**<br>
    `information_content = name.content.gsub("America is home to some of the most beautiful natural scenery in the world and while we definitely plan to indulge in the hot dogs, fireworks, and red white and blue everything, we think the best way to celebrate The Fourth of July is going out for a hike with friends and family. So head out on one of America's 25 Best Hikes or hit up your favorite local trail and celebrate the holiday weekend by getting outside!", "").gsub("Photo: Nicola Easterby", "").gsub("Photo: Mikaela Tangeman", "").gsub("Photo: Derrick Lyttle", "").gsub("Photo: Jessica Dales", "").gsub("Photo: Steve Yocom", "").gsub("Photo: Derek Cook", "").gsub("Photo: Christin Healey", "").gsub("Photo: Bo Baumgartner", "").gsub("Photo: Michael Matti", "").gsub("Photo: Adam Riquier", "").gsub("\n\n\n\n", "")`<br>
    `information_arr << information_content` **--This is where I used gsub to take out all of the useless information that I didn't want**<br>
   ` break if i == 10;`<br>
    `end`<br>
    `information_arr.shift`<br>
   ` information_arr[number]`** --Here I return the array with the argument that is supplied in my title method**<br>
  `end`<br>

## The Take away
After finishing this project I realized how important writing clear semantic HTML is and seperating your sections properly, especially if somebody is trying to steal all of your html :D!
