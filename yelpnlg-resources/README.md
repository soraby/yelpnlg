
The YelpNLG Corpus for Style in NLG
===================================
_Paper: "Curate and Generate: A Corpus and Method for Joint Control of Semantics and Style in Neural NLG." ACL 2019._
_Authors: Shereen Oraby, Vrindavan Harrison, Abteen Ebrahimi, and Marilyn Walker_


Description
-----------

The YelpNLG corpus provides training data for natural language generation of restaurant reviews,
specifically targeting end-to-end neural natural language generators.

The corpus consists of around 300,000 MR-to-NL (meaning representation to natural language reference)
automatically constructed using freely available restaurant reviews from Yelp.  The sentences all mention at least one
"meat" food value for semantic constraint. MRs include semantic information as well as a novel
characterization of descriptive lexical choice, sentiment, length, personal pronouns, and exclamations.

Parsing was done using Stanford CoreNLP, and sentence tokenization was done using NLTK:
https://stanfordnlp.github.io/CoreNLP/
https://www.nltk.org/

Please refer to the associated paper for more information about the corpus.


Contents
--------

**YelpNLG-Corpus**

The corpus is split into train, dev, and test sets (in the "yelpnlg-corpus" directory).

Each split file is a CSV containing a sequence of instances, each in the following format:
[id, ref, mr, sentiment, length, first_person, exclamation]

Each segment is described below:
* id - A sequential identifier of the instance in that split.
* ref - The reference text (review sentence) for that instance.
* mr - The meaning representation (mr) for that instance. Each MR is a set of space-separated tuples, and each is tuple
is divided with "||" separators. Each tuple contains the following information (in this order):
    * attribute - one of: {"restaurant", "cuisine", "food", "service", "staff", "ambiance", "price"}
    * value - any value (from attribute lexicons)
    * adjective - any adjective (from sentence dependency parse), else "no_adj" if none is available/retrievable in the parse
    * mention - mention_N (N indicates which mention is being referenced, i.e. 1 for first mention, 2 for second mention, etc.)
* sentiment - "positive" (4-5 stars), "neutral" (3 stars), "negative" (1-2 stars)
* length - "len_short" (4-10 tokens), "len_medium" (10-20 tokens), "len_long" (20-30 tokens)
* first_person - "first_person" (includes a first person pronoun: {"i", "my", "me", "our", "we", "us"}), "not_first_person" (does not include any first person pronouns)
* exclamation - "has_exclamation" (include an exclamation mark), "no_exclamation" (does not include an exclamation mark)

Note: In the experiments in the associated paper, we created different versions of the corpus to explore the effect of
more detailed style encoding. Specifically, we created 4 versions of the corpus, modifying the information available
in the "mr" segment:
* BASE - MR tuples only include attributes and their values (no other style variables)
* ADJ - MR tuples include attributes, values, and adjectives (no other style variables)
* SENT - MR tuples include attributes, values, adjectives, and sentiment (no other style variables)
* STYLE - MR tuples include all information: attributes, values, adjectives, sentiment, mention, length, first_person, exclamation

Additionally, note that while only the STYLE corpus version includes "mention", we include it in the "mr" tuples
directly in this released version of the corpus for clarity since it is an attribute-level variable. The other
variables, "sentiment", "length", "first_person", and exclamation are sentence-level variables and thus presented
separately from the "mr".


**YelpNLG-Lexicons**

The lexicons are an archive of 6 text files (in "yelpnlg-lexicons"), one for each attribute of interest
(ambiance, cuisine, food, price, restaurant, service, and staff). Each file contains a set of values for the
given attribute, one per line. Some values define a particular instance of the attribute, while others define a
way to lexicalize the attribute. Details for how the lexicons were created can be found in the paper. An
example SPARQL query for retrieving foods is given below:

```sql
# Sample SPARQL query for foods from DBPedia (https://dbpedia.org/sparql)
SELECT *
WHERE {
?fooda dbo:ingredient ?foodb .
?fooda rdfs:label ?namea .
FILTER (langMatches(lang(?namea), "en")) . 

?foodb rdfs:label ?nameb .
FILTER (langMatches(lang(?nameb), "en")) . 
}
LIMIT 10000 OFFSET 0
```

Citing
------

If you use this data in your research, please refer to and cite:  

"Curate and Generate: A Corpus and Method for Joint Control of Semantics and Style in Neural NLG." S. Oraby, V. Harrison, A. Ebrahimi, and M. Walker. ACL 2019.

