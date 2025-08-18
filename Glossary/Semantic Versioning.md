---
tags:
  - software
  - foss
  - conventions
definition: A software versioning specification
---
# Definition
Semantic Versioning is a method for tracking and naming iterations of a software package. In short, it's a number comprised of three digits separated by periods:
```
0.0.1
```
- The last digit ("PATCH version") is incremented for every backwards-compatible bug fix.
- The middle digit ("MINOR version") is incremented for every backwards-compatible feature implementation.
- The first digit ("MAJOR version") is increment for every change that makes the package _incompatible_ with previous versions. 

Read in-depth specifications at https://semver.org