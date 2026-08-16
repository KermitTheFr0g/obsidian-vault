---
type: project
tags:
  - self-development
  - studying
---
# Overview
This document outlines all of the different topics that I am currently studying and what I am working through. Also potential topics I want to research or learn about in the future.
# Categories
## Computer Science

```dataview
TABLE WITHOUT ID file.link AS "Topic", status AS "Status"
FROM "5. Topics"
WHERE type = "study-topic" AND category = "computer-science"
SORT choice(status = "in-progress", 0, choice(status = "not-started", 1, 2)) ASC, file.name ASC
```

## History

```dataview
TABLE WITHOUT ID file.link AS "Topic", status AS "Status"
FROM "5. Topics"
WHERE type = "study-topic" AND category = "history"
SORT choice(status = "in-progress", 0, choice(status = "not-started", 1, 2)) ASC, file.name ASC
```

## Writing

```dataview
TABLE WITHOUT ID file.link AS "Topic", status AS "Status"
FROM "5. Topics"
WHERE type = "study-topic" AND category = "writing"
SORT choice(status = "in-progress", 0, choice(status = "not-started", 1, 2)) ASC, file.name ASC
```