## Spiders

Learn to create web crawlers with scrapy. These scrapy spiders will crawl the web through multiple pages, following links to scrape each of those pages automatically according to the procedures we've learned in the previous chapters.

<br>

### Inheriting the Spider

```
# Import scrapy library
import scrapy

# Create the spider class
class YourSpider(scrapy.Spider):
  name = "your_spider"
  # start_requests method
  def start_requests(self):
    pass
  # parse method
  def parse(self, response):
    pass
  
# Inspect Your Class
inspect_class(YourSpider)
```

### Hurl the URLs

```
# Import scrapy library
import scrapy

# Create the spider class
class YourSpider(scrapy.Spider):
  name = "your_spider"
  # start_requests method
  def start_requests(self):
    urls = ["https://www.datacamp.com","https://scrapy.org"]
    for url in urls:
      yield url
  # parse method
  def parse(self, response):
    pass
  
# Inspect Your Class
inspect_class(YourSpider)
```

### Self Referencing is Classy

```
# Import scrapy library
import scrapy

# Create the spider class
class YourSpider(scrapy.Spider):
  name = "your_spider"
  # start_requests method
  def start_requests(self):
    self.print_msg("Hello World!")
  # parse method
  def parse(self, response):
    pass
  # print_msg method
  def print_msg(self, msg):
    print("Calling start_requests in YourSpider prints out:", msg)
  
# Inspect Your Class
inspect_class(YourSpider)
```

### Starting with Start Requests

```
# Import scrapy library
import scrapy

# Create the spider class
class YourSpider(scrapy.Spider):
  name = "your_spider"
  # start_requests method
  def start_requests(self):
    yield scrapy.Request(url="https://www.datacamp.com", callback=self.parse)
  # parse method
  def parse(self, response):
    pass

# Inspect Your Class
inspect_class(YourSpider)
```

### Pen Names

```
# Import the scrapy library
import scrapy

# Create the Spider class
class DCspider(scrapy.Spider):
  name = 'dcspider'
  # start_requests method
  def start_requests(self):
    yield scrapy.Request(url = url_short, callback = self.parse)
  
  # parse method
  def parse(self, response):
    # Create an extracted list of course author names
    author_names = response.css('p.course-block__author-name::text').extract()
    # Here we will just return the list of Authors
    return author_names
  
# Inspect the spider
inspect_spider(DCspider)
```

### Crawler Time

```
# Import the scrapy library
import scrapy

# Create the Spider class
class DCdescr(scrapy.Spider):
  name = 'dcdescr'
  # start_requests method
  def start_requests(self):
    yield scrapy.Request(url = url_short, callback = self.parse)
  
  # First parse method
  def parse(self, response):
    links = response.css('div.course-block > a::attr(href)').extract()
    # Follow each of the extracted links
    for link in links:
      yield response.follow(url = link, callback = self.parse_descr)
      
  # Second parsing method
  def parse_descr(self, response):
    # Extract course description
    course_descr = response.css('p.course__description::text').extract_first()
    # For now, just yield the course description
    yield course_descr


# Inspect the spider
inspect_spider(DCdescr)
```

### Time to Run

```
# Import scrapy
import scrapy

# Import the CrawlerProcess: for running the spider
from scrapy.crawler import CrawlerProcess

# Create the Spider class
class DC_Chapter_Spider(scrapy.Spider):
  name = "dc_chapter_spider"
  # start_requests method
  def start_requests(self):
    yield scrapy.Request(url = url_short,
                         callback = self.parse_front)

  # First parsing method
  def parse_front(self, response):
    course_blocks = response.css('div.course-block')
    course_links = course_blocks.xpath('./a/@href')
    links_to_follow = course_links.extract()
    for url in links_to_follow:
      yield response.follow(url = url,
                            callback = self.parse_pages)
  
  # Second parsing method
  def parse_pages(self, response):
    crs_title = response.xpath('//h1[contains(@class,"title")]/text()')
    crs_title_ext = crs_title.extract_first().strip()
    ch_titles = response.css('h4.chapter__title::text')
    ch_titles_ext = [t.strip() for t in ch_titles.extract()]
    dc_dict[crs_title_ext] = ch_titles_ext

# Initialize the dictionary **outside** of the Spider class
dc_dict = dict()

# Run the Spider
process = CrawlerProcess()
process.crawl(DC_Chapter_Spider)
process.start()

# Print a preview of courses
previewCourses(dc_dict)
```

### DataCamp Descriptions

```
# Import scrapy
import scrapy

# Import the CrawlerProcess: for running the spider
from scrapy.crawler import CrawlerProcess

# Create the Spider class
class DC_Description_Spider(scrapy.Spider):
  name = "dc_chapter_spider"
  # start_requests method
  def start_requests(self):
    yield scrapy.Request(url = url_short,
                         callback = self.parse_front)
  
  # First parsing method
  def parse_front(self, response):
    course_blocks = response.css('div.course-block')
    course_links = course_blocks.xpath('./a/@href')
    links_to_follow = course_links.extract()
    for url in links_to_follow:
      yield response.follow(url = url,
                            callback = self.parse_pages)
  
  # Second parsing method
  def parse_pages(self, response):
    # Create a SelectorList of the course titles text
    crs_title = response.xpath('//h1[contains(@class,"title")]/text()')
    # Extract the text and strip it clean
    crs_title_ext = crs_title.extract_first().strip()
    # Create a SelectorList of course descriptions text
    crs_descr = response.css('p.course__description::text')
    # Extract the text and strip it clean
    crs_descr_ext = crs_descr.extract_first().strip()
    # Fill in the dictionary
    dc_dict[crs_title_ext] = crs_descr_ext

# Initialize the dictionary **outside** of the Spider class
dc_dict = dict()

# Run the Spider
process = CrawlerProcess()
process.crawl(DC_Description_Spider)
process.start()

# Print a preview of courses
previewCourses(dc_dict)
```

### Capstone Crawler

```
# Import scrapy
import scrapy

# Import the CrawlerProcess
from scrapy.crawler import CrawlerProcess

# Create the Spider class
class YourSpider(scrapy.Spider):
  name = 'yourspider'
  # start_requests method
  def start_requests(self):
    yield scrapy.Request(url = url_short, callback=self.parse)
      
  def parse(self, response):
    # My version of the parser you wrote in the previous part
    crs_titles = response.xpath('//h4[contains(@class,"block__title")]/text()').extract()
    crs_descrs = response.xpath('//p[contains(@class,"block__description")]/text()').extract()
    for crs_title, crs_descr in zip( crs_titles, crs_descrs ):
      dc_dict[crs_title] = crs_descr
    
# Initialize the dictionary **outside** of the Spider class
dc_dict = dict()

# Run the Spider
process = CrawlerProcess()
process.crawl(YourSpider)
process.start()

# Print a preview of courses
previewCourses(dc_dict)
```