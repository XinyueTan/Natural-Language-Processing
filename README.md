# Natural Language Processing

## Goal of the analysis

In this project, I will completing three main tasks. Processing a set of documents, running a sentiment analysis of thise documents and then generating topic models of those documents by applying latent dirichlet allocation. The documents I will be using will be student notes that the "class HUDK4050" in Teachers College, Columbia University made last semester. 

## Packages Required
```
install.packages("tm")
install.packages("SnowballC")
install.packages("wordcloud")
install.packages("topicmodels") 
install.packages("dplyr")
install.packages("tidyr")
```
## Procedures
### Making Wordcloud

1. Import all document files and then list of weeks file
2. Clean the html tags from the text
3. Process text using **tm package** with alternative processing.
  * Convert the data frame to the corpus format used in tm package
  * Remove spaces, pre-defined stop words ('the', 'a', etc...), numbers and punctuation
  * Convert upper case to lower case, words to stems for analysis
  * Convert corpus to a term document matrix so that each word can be analyzed indiviudally
4. Find common words by creating a data frame of word frequencies
``` 
[1] "abil"         "across"       "action"       "actor"        "algorithm"    "also"         "alway"        "amp"         
[9] "analysi"      "analysis"     "analyt"       "analytics"    "analyz"       "approach"     "articl"       "assess"      
[17] "author"       "averag"       "base"         "best"         "better"       "build"        "call"         "can"         
[25] "chang"        "class"        "clear"        "cluster"      "cognit"       "collect"      "combin"       "compar"      
[33] "comput"       "concept"      "connect"      "construct"    "correl"       "cours"        "creat"        "data"        
[41] "dataset"      "decis"        "defin"        "describ"      "design"       "develop"      "differ"       "difficult"   
[49] "discoveri"    "edm"          "educ"         "education"    "effect"       "error"        "ethic"        "evalu"       
 ```
5. Generate a **word cloud** 
  * scale: controls the size of the words (font)
  * max.words: indicates the maximum number of words to be plotted (if you omit this R will try to squeeze every unique word into the diagram!)
  * rot.per: indicates the porportion words with 90 degree rotation (vertical text)
  * random.colors: chooses colors randomly from the colors
 <img src="https://user-images.githubusercontent.com/46146748/63191023-8a716e00-c035-11e9-8b3e-d973acc4712e.png" width="600">
6. Merge with week list to have a variable representing weeks for each entry.
7. Create a Term Document Matrix and repeat step 5.

### Sentiment Analysis 
1. Match words in corpus to lexicons of **positive and negative words**
2. Generate an **overall pos-neg score** for each matched line between each word and the two lexicons
3. Geneate a visualization of the sum of the sentiment score over weeks with ggplot
<img src="https://user-images.githubusercontent.com/46146748/63191455-8265fe00-c036-11e9-82a8-2196c1e89590.png" width="600">

### LDA Topic Modelling
1. Term Frequency Inverse Document Frequency
2. Remove very uncommon terms (TFID freq < 0.1)
3. Remove non-zero entries, find the sum of words in each document, and divide by sum across rows
4. Find out the most common terms in each topic 
```
Topic 1   Topic 2   Topic 3   Topic 4   Topic 5 
   "data"    "data" "network"   "model"    "data" 
```
5. Find out which documents belong to which topic
6. Generate a *single* visualization showing: 
- Sentiment for each week and 
- One important topic for that week
<img src="https://user-images.githubusercontent.com/46146748/63193248-fbffeb00-c03a-11e9-980e-cdf7000e0df4.png" width="600">

## Background
The use of natural language processing has exploded over the last decade. Appilcations that require machines to understand natural human speech patterns are abundant and substantial improvements in these systems has increased their utility. 

Within the educational space NLP is used to interpret human speech for the prupose of understanding human problems and recently an online tutor passed a limited version of the [Turing Test](https://en.wikipedia.org/wiki/Turing_test) when it was [indistinguishable from teaching assistants in a college class](http://www.news.gatech.edu/2017/01/09/jill-watson-round-three).

For example, **intellectual tutoring system** resided in the NLP are designed to assess essay quality and guide feedback to students. It considers a broad array of linguistic, rhetorical, and contextual feature. [McNamara, D. S., Crossley, S. A., & Roscoe, R. (2013). Natural Language Processing in an Intelligent Writing Strategy Tutoring System. Behavior Research Methods, 45(2), 499–515.](http://link.springer.com.ezproxy.cul.columbia.edu/article/10.3758/s13428-012-0258-1)

The algorithm assesses the followings:
      * lexical (e.g.: lexical sophistication, word frequency lexical types)
      * syntactic (e.g.: the number of words before the main verb)
      * cohesion (several dimensions of cohesion including coreferential cohesion, causal cohesion, density of connectives, temporal cohesion, spatial cohesion, and latent semantic analysis)
      * rhetorical
      * reading ease indices 


## Definitions and concepts
1. **Supervised machine learning**: each item in the training data (typically a vector) is labeled with a desired output value (also called the supervisory signal). 
    * Classification come under supervised learning

2. **Unsupervised machine learning**: used to draw inferences from datasets consisting of input data without labeled responses. 
    * Cluster analysis, which is used for exploratory data analysis to find hidden patterns or grouping in data.

3. **Overfitting**:  is a modeling error which occurs when a function is too closely fit to a limited set of data points, but make poor predictions for new, previously unseen cases. This is because it may learn the random noise in the training data rather than only its essential, desired features. 

4. **Cross-validation**: technique used to minimize overfitting risks. It partitions the example data randomly into training and test sets to internally validate the model's predictions. This process of data partitioning, training, and validation is repeated over several rounds, and the validation results are then averaged across rounds.
    * **K-fold cross validation** is a resampling procedure used to validate machine learning models on a limited data sample. K refers to the number of groups that a given data sample is to be split into.
    
   **Procedure**: 
      1. shuffle the dataset randomly 
      2. split the dataset into k groups 
      3. take the group as a hold out and take the remaining groups as a training data set, fit a model on the training set and evaluate it ont the test set, retain the evaluation score and discard the model 
      4. Summarize the skill of the model using the sample of model evaluation scores;parameter (coefficient): 1/k sum of the parameter (1+..+k)

## Related Readings
[Nadkarni, P. M., Ohno-Machado, L., & Chapman, W. W. (2011). Natural language processing: An Introduction. Journal of the American Medical Informatics Association: JAMIA, 18(5), 544–551.](http://www.ncbi.nlm.nih.gov/pmc/articles/PMC3168328/)

[Robinson, A. C. (2015). Exploring Class Discussions from a Massive Open Online Course (MOOC) on Cartography. In J. Brus, A. Vondrakova, & V. Vozenilek (Eds.), Modern Trends in Cartography (pp. 173–182). Springer International Publishing.](http://link.springer.com.ezproxy.cul.columbia.edu/chapter/10.1007/978-3-319-07926-4_14)

[McNamara, D. S., Crossley, S. A., & Roscoe, R. (2013). Natural Language Processing in an Intelligent Writing Strategy Tutoring System. Behavior Research Methods, 45(2), 499–515.](http://link.springer.com.ezproxy.cul.columbia.edu/article/10.3758/s13428-012-0258-1)

[Quora. (2017). What is a good explanation of Latent Dirichlet Allocation?](https://www.quora.com/What-is-a-good-explanation-of-Latent-Dirichlet-Allocation)


## Videos

[Crash Course. (2017). Natural Language Processing.](https://www.youtube.com/watch?v=fOvTtapxa9c)

[Raval, S. (2016). Sentiment Analysis in 4 Minutes.](https://www.youtube.com/watch?v=AJVP96tAWxw)

[Knispelis, A. (2016). LDA Topic Models.](https://www.youtube.com/watch?v=3mHy4OSyRf0)


## Author
[Katherine Tan](www.linkedin.com/in/katherine-tan-2019), M.S student in Learning Analytics at Teachers College, Columbia University

