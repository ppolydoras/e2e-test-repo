# Description
This utility generates a list of topics that relate to a given term, based on a search on a given list of greek news sites. The list can be found here:
```s3://rawlabs-public-test-data/competition/pp/topic-modelling/rss-feeds.csv```
Feel free to add new RSS feeds, but this may cause instability..

The search process is the following:
1. Read all RSS feeds and filter out those with descriptions that do not contain the given search term
2. Access the actual webpages of the related feeds
3. Get greek only content
4. Filter out greek stopwords
5. Find top-N most frequently used terms

# Prerequisites
- Access to RAW UI
- Knowledge of Greek
- Bash with curl and jq installed
- Patience

# Usage
The generic syntax is the following:
```curl -v 'https://<hostname>/arsenal/v1/topic-extraction?term=<search_term>&topN=<top_n>'```
E.g.
```curl -v 'https://<hostname>/arsenal/v1/topic-extraction?term=ΚΙΝΑΛ&topN=25'  | jq .```

At the time of writing these lines, the results are the following:
```
[
  "ελλάδα",
  "χπα",
  "νέα",
  "μετοχών",
  "δεικτών",
  "κιναλ",
  "δόση",
  "χαρτοφυλάκια",
  "ελλαδα",
  "αγοράς",
  "πράξεις",
  "γραφήματα",
  "χα",
  "ισοτιμίες",
  "αεκ",
  "όπως",
  "αναζήτηση",
  "εκλογές",
  "κύπελλο",
  "εγγραφή"
]
```

Another example is:
```
http://localhost:54325/arsenal/v1/topic-extraction?term=Ολυμπιακός&topN=20
```
Results:
```
[
  "χπα",
  "ελλάδα",
  "δεικτών",
  "μετοχών",
  "νέα",
  "αεκ",
  "κιναλ",
  "δόση",
  "χαρτοφυλάκια",
  "λάρισα",
  "αγοράς",
  "πράξεις",
  "γραφήματα",
  "χα",
  "ισοτιμίες",
  "αναζήτηση",
  "εκλογές",
  "εγγραφή",
  "ελλάδας",
  "ολυμπιακός"
]
```


# TODO
Many improvements such as HTML parsing/processing, stopwords removal and topic generation algorithm. From the user perspective, the most problematic part is backend timeouts, which cannot be controlled by the client. So, feel free to make an initial call, then wait for half a minute and then repeat it. You should be able to see results.
