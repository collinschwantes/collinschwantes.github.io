---
layout: post
title: Make your published code more useful 
date: 2026-04-30 01:39:00
tags: code FAIR RSE
description: Share code so that it can be used
featured: true
mermaid:
  enabled: true
  zoomable: true
---

Today I came across a paper on range shifts in a common genus of birds that had a full data and code sharing section.
It made my little data librarian heart pitter patter to see such a complete accounting of where data came and where the code to run the paper's analysis lives. 

Then I looked at the links. GBIF data can be obtained from GBIF.org. IUCN redlist data can be downloaded at IUCN.org. 
Those are big websites my friend, thats like saying I can be found in North America. 
I've already written about quick wins for sharing data [here](https://collinschwantes.github.io/blog/2025/data-quick-wins/) so we will brush that aside. 

Lets take a look at the repo - maybe the persistent digital identifiers can be found in the code? Nope!
The repo is a collection of R scripts that read and write data to folders outside the repo. Oh boy.  

Lets learn from that author's mistakes. 

### 1 Your project should have a readme that explains the project's aims and how to run the code

A minimal example readme: 

This project aims to simulate range shifts for coyotes under various climate and urbanization scenarios while rigorously accounting for observational bias. 

The analyses for this project were run in R version 4.6.1 on a high performance compute cluster at Yale University. 

To execute the code, run the `"execute_code.R"` file. Be aware that this analysis will take approximately 50 hours on a computer with 16 gbs of ram. 

This repo contains the following folders: ..... describe the folders
For published results see: DOI.TO.PAPER
For metadata see: Data dictionary in data folder (maybe you've got a datapackage.json file in your zenodo deposit, who knows)

### 2 The code for your project should be self contained. 

```
--| Coyote_URCLI
  |-- Data
  |-- Figures
  |-- R
  |-- Scripts
  |-- execute_code.R
```
Your project folder should contain or be able to create all the files^a^ necessary for running your analysis. 
If you're code reads from or writes to a location outside the project folder, thats a problem for anyone else trying to run your code.

Since everything is contained in the top project folder (e.g. `Coyote_URCLI`) its clear that is the intended working directory. All file and folder paths can then be relative to your project folder (e.g. `./R` instead of `User/Desktop/Research/Mammals/year2/code/final_final/Coyote_URCLI/R`). 

**YOU SHOULD NOT NEED TO SET THE WORKING DIRECTORY FOR OTHERS.** 

a. If you have sensitive data or other sharing restrictions on data this Rule of thumb can't be met. But you would note that in the readme and maybe provide dummy data. 

### 3 Your code should be documented

You don't need to use a formal documentation framework, in line comments go a long way towards communicating whats supposed to be happening in a given code chunk.

Let's take a peak at `execute_code.R`

```
# load necessary libraries
library(tidyverse)
library(vegan)
library(netlogoR)
library(fs)

## source all functions from R
for(i in fs::dir_ls("R")){
  source(i)
}

# run data processing script
source("Scripts/data_processing.R")

# run simulation - this takes awhile. 
source("Scripts/simulation.R")

# precompiled simulation data is available here: zenodo.org/fake/sim/deposit
# source("Scripts/read_sim_results.R")

# create figures
source("Scripts/create_figures")
```

Its a simple script that loads all libraries necessary for executing the code, sources all the functions used in the scripts, tells a user what order to run the R scripts in, and gives a brief description of what each script does. 


### 4 Run the code in a clean environment

Before sharing your code, make sure your code runs from a clean session - this is especially important for R users
where objects can persist between session in the `.Rdata` file. 


### 5 Run the code on NOT your computer 

Send your code to someone else and have them run in it on their machine. 
This can be as simple as zipping the project folder and passing it over to another person's computer. 
They unzip the folder and try to run the code. If it works - awesome! 

If it doesn't, figure out what undocumented dependencies you have or if you've accidentally hard coded paths somewhere or if you have an object in your R session that doesn't exist on the other computer.





