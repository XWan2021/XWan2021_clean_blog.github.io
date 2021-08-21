---
layout: post
title: "Web Scraping in R"
subtitle: "scraping moive data from IMDB"
background: '/img/posts/web-scraping/1.png'
---


## Installing packages
```
library(rvest)
library(dplyr)
```
## Webpage
![IMDB page](/img/posts/web-scraping/imdb_screenshot.png)

## Scraping the ata
```
link = "https://www.imdb.com/search/title/?title_type=feature&num_votes=25000,&genres=adventure&sort=user_rating,desc"
page = read_html(link)

name = page %>% html_nodes(".lister-item-header a") %>% html_text()
year = page %>% html_nodes(".text-muted.unbold") %>% html_text()
rating = page %>% html_nodes(".ratings-imdb-rating strong") %>% html_text()
synopsis = page %>% html_nodes(".ratings-bar+ .text-muted") %>% html_text()
```
## Writing to a .csv
```
movies = data.frame(name, year, rating, synopsis, stringsAsFactors = FALSE)
write.csv(movies, "movies.csv")
```