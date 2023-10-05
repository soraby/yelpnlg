# YelpNLG: Review Corpus for NLG
This page was migrated from https://nlds.soe.ucsc.edu/yelpnlg

**If you use this data in your research, please refer to and cite**:   [Curate and Generate: A Corpus and Method for Joint Control of Semantics and Style in Neural NLG](https://aclanthology.org/P19-1596/). S. Oraby, V. Harrison, A. Ebrahimi, and M. Walker. ACL 2019. Florence, Italy.

## Overview
YelpNLG provides resources for natural language generation of restaurant reviews. The corpus consists of ~300,000 MR-to-NL (meaning representation to natural language reference) created using freely available restaurant reviews from Yelp.  MRs include semantic information as well as a novel characterization of descriptive lexical choice, sentiment, length, personal pronouns, and exclamations. The lexicons include a set of values instantiating popular attributes from the restaurant domain, e.g. cuisine or food.

## Data
The corpus available for download is a set of 3 CSVs containing the instances in the train, dev, and test splits. Each instance includes a reference, MR, and a set of style variables. The README includes data formatting details.

## Lexicons
The lexicons available for download are a set of 6 text files, one for each attribute of interest (ambience, cuisine, food, price, restaurant, service, and staff). Each file contains a set of values for the given attribute, one per line.