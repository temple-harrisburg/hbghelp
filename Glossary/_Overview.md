---
tags:
  - glossary
  - help
---
# Overview
This folder contains common terms and definitions used in the IT department at Temple Harrisburg. 

## Structure
Each term is its own markdown file, with the exclusion of some files which are lists of common terms within a given topic.

# Terms
```dataview
TABLE WITHOUT ID file.link AS "Term", definition AS "Definition"
FROM "Glossary"
WHERE !startswith(file.name, "_")
```