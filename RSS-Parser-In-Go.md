---
title: RSS Parser In Go
date: 25-06-2022
private: false
---

```go
import (
  "encoding/xml"
  "fmt"
  "net/http"
)

type Enclosure struct {
  Url    string `xml:"url,attr"`
  Length int64  `xml:"length,attr"`
  Type   string `xml:"type,attr"`
}

type Item struct {
  Title     string    `xml:"title"`
  Link      string    `xml:"link"`
  Desc      string    `xml:"description"`
  Guid      string    `xml:"guid"`
  Enclosure Enclosure `xml:"enclosure"`
  PubDate   string    `xml:"pubDate"`
}

type Channel struct {
  Title string `xml:"title"`
  Link  string `xml:"link"`
  Desc  string `xml:"description"`
  Items []Item `xml:"item"`
}

type Rss struct {
  Channel Channel `xml:"channel"`
}

func getRss(url string) (r Rss) {
  resp, err := http.Get(url)
  if err != nil {
    fmt.Printf("Error GET: %v\n", err)
    return
  }
  defer resp.Body.Close()

  rss := Rss{}

  decoder := xml.NewDecoder(resp.Body)
  err = decoder.Decode(&rss)
  if err != nil {
    fmt.Printf("Error Decode: %v\n", err)
    return
  }

  return rss
}

func main() {
  rss := getRss("https://hackernoon.com/feed")

  fmt.Println(rss.Channel.Title)
  for i, item := range rss.Channel.Items {
    fmt.Printf("%d. %s\n", i, item.Title)
  }
}
```
