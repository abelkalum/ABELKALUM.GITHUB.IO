---
layout: post
title:      "Scraping Data with Repl.it"
date:       2020-03-20 18:42:01 -0400
permalink:  scraping_data_with_repl_it
---


So, for the last few weeks I have been fascinated at how iteration over an array makes the code drier and cleaner. I have learned that it is important to remember that if we are to use indexes, we should always remember to set the counter to start at 0 first element in an array has an index of 0.
During scraping, if the final stage of the scraping process is to get details for each category or section items scraped, it is important to come up with an iteration method that passes each item (example: History museums in Boston) through the block to get the item details (example: name, review, and rating of each History museum in Boston). To be able to do this one could use repl.it website to get initial part of the scraping method set, then use binding.pry at the terminal to confirm if the lines of code work. Below is an example of the second part of scraping I did for my project, in this case the method shown here is intended to scrape the details of each museum:

```
def self.scrape_museums(category)
    url = "https://www.tripadvisor.com/Attractions-g60745-Activities-c49-Boston_Massachusetts.html"
    webpage = Nokogiri::HTML(open(url))
    museums = webpage.css("div div.listing_details")
    
    museums.each do |card| 
      #creating an instance  
      museums = BostonMuseums::Museum.new  

      #assigning object attributes

      museum.name = card.css("div.listing_title.title_with_snippets h2").text
      museum.review = card.css("div.prw_rup.prw_attractions_attractions_review_snippets").text
      museum.rating  = card.css("div.listing_rating").text

      category.museums << museum
   end
  end
 end
```

Back to repl.it we enter:
require "nokogiri"
require "open-uri"

url = "https://www.tripadvisor.com/Attractions-g60745-Activities-c49-Boston_Massachusetts.html"
webpage = Nokogiri::HTML(open(url))
museums = webpage.css("div div.listing_details")[0].text().strip

The above will give you the object attributes data of each of the museums; that is the museum’s name, review, and rating.

Enjoy your coding day!

