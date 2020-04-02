---
layout: post
title:      "Many Moving Parts / Objects"
date:       2020-04-02 00:27:23 +0000
permalink:  many_moving_parts_objects
---


The BostonMuseums CLI that I build provides information about top-rated museums in Boston. Through it, for each museum, one can access the museum’s details like its rating, URL, and one or two review snippets. 
It was with a lot of trepidation that I began this CLI project. First off, I had rushed to complete my labs leading to this first project that I was almost burned out. My plan was to spend more time on the project so that I could build a dazzling CLI. I visualized that if I had four separate classes (Scraper, Museums, CLI, & Category), this would at least allow me to easily scrape data two levels deep. That is scrape for categories of museums, then the museums in each category, and finally the details of each museum. I was wrong, this was no easy task. It proved difficult to get the objects in separate classes to relate. So many errors on methods! So many moving parts that need to be connected for the CLI to work! I finally trimmed my classes to three (Scraper, Museums, & CLI). I then settled on scraping museum links and names at first level, then for each museum scrape for data to assign to the attributes of Museums class instances like its rating, review snippets, and URL. 
Another challenge I had was the dependencies I was using. My original scraping plan was how to get to the URL of each category using Nokogiri, then use the category_URLs obtained to scrape for museums and their details. At this point, I was thinking of a Scraper class with two methods: one for categories and the other for museums. I got stuck after scraping the original website URL for the names of the various categories of museums. In order to resolve this impasse, I finally decided to use HTTParty in addition to Nokogiri to get the scraping done with fewer lines of code.
 
```
class BostonMuseums::Scraper

  attr_accessor :museum_list_url

   BASE_PATH = "https://www.tripadvisor.com"
   museum_list_url = (BASE_PATH + "/Attractions-g60745-Activities-c49-Boston_Massachusetts.html#FILTERED_LIST")

  def self.scrape_index_page(museum_list_url) 
      doc = HTTParty.get(museum_list_url)
      index = Nokogiri::HTML(doc)
      scraped_museums = index.css(".listing_details")
      scraped_museums.collect do |museum_content|
         {
          :name => museum_content.css("div.listing_title.title_with_snippets h2").text().strip,
          :museum_site_url => BASE_PATH + museum_content.css("a").attribute("href").value,
          :museum_rating => museum_content.css("div.popRanking.wrap").text().strip,
          :museum_review_snippets => museum_content.css("div.prw_rup.prw_attractions_attractions_review_snippets").text().strip
        }
  end
 end
end
```


After spending many hours working on this project, I must admit that I got better in cloning my Github repository, adding changes, committing the changes, then pushing the changes to the Github repository. I got better at reading and correcting errors too. It was fun using the element inspector to manually look for CSS selectors, then use Repl.it website to check if the CSS selectors will grab object attributes from the HTML document. I believe that next time I can build a scraper which can scrape deeper for more data beyond the first level.

