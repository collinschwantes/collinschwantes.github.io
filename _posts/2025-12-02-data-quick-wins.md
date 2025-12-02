---
layout: post
title: Make your open data more useable 
date: 2025-12-02 01:39:00
tags: data publishing fair
description: Quick wins when publishing open data
featured: true
mermaid:
  enabled: true
  zoomable: true
---

Making open data more useful for yourself and others may be easier than you think. 
Here are some quick wins you can employ with every open dataset you publish. 

### 1. Include metadata for your data.
 This may be a schema or a data dictionary. Whatever form it takes, providing definitions for the fields in your data will make them immensely more useful. It is obvious to you, the person who has been working on this project the most, what each field means, but not to the rest of us. Metadata will also give you an opportunity to think critically about what each field means in your data and how best to describe it. Most importantly, metadata will give future you a better understanding of what these data mean when you come back to them in 6 months or a year. If you can, use a controlled vocabulary to define terms in your data. 

### 2. Include project metadata.
 Tell people who created the data, when, and how. Provide links to publications and protocols if applicable. This makes it much easier to contextualize the data and to find them via search. 

### 3. Put your data in a place people are likely to find it.
 If no discipline specific place exists, put it in a generalist repository like Zenodo, OSF, or Figshare. Github repositories are a good start but should not be a final location. 

### 4. Publish your data in a non-proprietary file format. 
  If you're creating tabular data, CSV's are a great way to store your data. If your data are too big for a CSV, consider [parquet](https://parquet.apache.org/).

### 5. It may be 2025, but keep punctuation (except underscores) and emojis out of column headers/field names.
 Why? Because punctuation and emojis make basic tools like regular expressions harder to use. 
 Many programming languages interpret things like `!`, `.`, `$`, or `?` in a particular way and having to code around them creates friction. Even seemingly simple characters like the humble dash can be tricky ([unicode dash encodings](https://www.compart.com/en/unicode/category/Pd)). Emojis may be unicode but they are often compound unicode characters `person + dance + skin-color-2`, which can cause inscrutable encoding errors or unexpected issues.    

### 6. Use consistent styling in your column headers.
 `snake_case` and `camelCase` are nice because they are human and machine readable. Having inconsistent styling means users are more likely to commit typographical errors. 

### 7. When applicable, use persistent digital identifiers.
When applicable, use persistent digital identifiers (PIDs) like DOIs, [ORCIDs](https://orcid.org/), [ROR ids](https://ror.org/) or permanent URLS when referencing outside resources. If you have a database of journal articles, include the DOIs to make referencing the articles faster.  A lot of metadata about a journal article can be extracted if you have the DOI handy. 
