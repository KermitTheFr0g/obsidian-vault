---
type: project
tags:
  - blog
---
# Overview
This project is just me writing about anything, it could be a book review, my thoughts, something to do with software or tech. Anything that I find interesting enough to want to talk about.

# Journal Entries
```dataview
TABLE WITHOUT ID file.link AS "Blog", status AS "Status"
FROM "7. Main Notes"
WHERE type = "journal"
SORT choice(status = "in-progress", 0, choice(status = "not-started", 1, 2)) ASC, file.name ASC
```

# Journal Ideas
