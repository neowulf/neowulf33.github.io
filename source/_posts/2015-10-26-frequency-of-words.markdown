---
layout: post
title: "Frequency Of Words"
date: 2015-10-26 21:10:10 -0700
comments: true
categories: scala
---

## Abstract ##

I want to demonstrate the power of Scala allowing us to comprehend lists in an easy fashion. 

*Note: 
this post is only for illustration purposes as this solution can also be done entirely in ElasticSearch.*

<!--more-->

### Step 1 ###

Generate a comma separated list of words from the JSON document.

```
curl 'localhost:9200/curated/_search?q=*:*&fields=keywords&size=30' \
  | jq '.hits.hits[] | .fields.keywords' \
  | tr '\n' ' '     \
  | tr '[' '\n'     \
  | tr ']' ','      \
  | sed 's|null||g' \
  > /tmp/keywords.scala
```

The following tools were used to generate a comma separated list of words.

1. `jq` - lightweight and flexible command-line JSON parser. [Documentation](https://stedolan.github.io/jq/)
    * `.hits.hits[]` - Get the array of `hits`.
    * `.fields.keywords` - Get the `keywords` from each of the `hits` and return the results in an array.
2. `tr` - linux utility which translates a single character. [Documentation](http://linux.die.net/man/1/tr)
    * Replace the newlines and the braces into a comma separated list of words. 
3. `sed` - popular linux utility which is an acronym for stream editor. [Documentation](http://linux.die.net/man/1/sed)
    * Delete `null` words. 

#### Step 2 ####

Prepend the result from the previous command with `List(` and append with `)`. I used
a scala worksheet to play around with the list of keywords.

```
List("chicken", "barn", "dog", "cowboy", "farmers", "country", "rural" ,
  "beach", "beaches", "sunrise", "sunrises", "emerald isle", 
  "emerald isle nc", "north carolina", "north carolina beach", 
  "sunrise over the beach", "atlantic ocean" ,"german shepherd", 
  "dog", "portrait", "pet", "pets", "original painting", "realism", 
  "l.a.shepard", "puppy", "canine", "pine", "scene", "landscape"
).foldLeft(Map.empty[String, Int]) { (acc, currentItem) =>
  acc + (currentItem -> (acc.get(currentItem).getOrElse(0) + 1))
}.toList.sortBy { entry =>
  - entry._2
}.foreach{ case (key, value) =>
  println(value.toString + "  " + key)
}
```

Salient Points

1. Iterate through the list and calculate the word frequency.
2. Needed to reverse sort the values.

