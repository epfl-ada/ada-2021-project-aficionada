# ADA made me famous!

## Abstract
### “Shoot for the moon. Even if you miss, you'll land among the stars.” Norman Vincent Peale

Did you ever dream of your words like the ones of Shakespeare, Einstein, or Trump remaining forever etched in the memory of humanity?  Would you like to be famous? Then this project might help you!

We decided to explore what makes a famous quote. Is it its length? It’s topic? Or something only a proper EDA could reveal? The idea is to study a maximum number of features of quotes evaluated as ‘famous’ in order to try to characterize the perfect quote. Maybe this study will reveal some hidden patterns about them. Combined with Machine Learning (ML) and Natural Language Processing(NLP), we could create a perfect quote generator and try to become famous thanks to ADA!

The main findings of this project can be found on the following website: https://manoui.github.io/website/

## Methods
You can find all the steps and methods detailed on the M3 notebook, if you are only interested in a specific part, use the index.

### Preprocessing and filtering
The notebook contains the performed preprocessing steps to obtain an exploitable and trustworthy dataset.

### Exploratory Data Analysis
Once the dataset was filtered and extended, we performed a univariate data analysis with summary statistics and graphical information on the distribution of each covariate in order to get a better understanding of the data and design a more complex data analysis.

Then, multivariate data analysis followed to understand the relation between the different covariates associated with a quote. We use scatterplots in order to understand the correlation between the different variables and barcharts with colored features to have a more complete insight into their relationship.


### Dataset enrichment
In order to enrich our dataset with new features, we needed to compute them using available methods. The first thing we extracted was the number of words and characters in a quote. Then, some NLP methods allowed us to extract for instance the polarity and subjectivity of a quote, that is to say, its sentiment. We also computed the complexity of a sentence using the Gunning Fog score. Using Spacy, we identified the grammatical content of a sentence, that is to say, the number of NOUNS, VERBS, ADJECTIVES, etc. Entities present in the quote such as PERSON, PLACE, ORGANIZATION were also counted.

We tried to retrieve the topic of a quote in order to see if a specific theme is more plebiscite than others. We decided to use a text analysis tool named Empath, which was the most promising kind of analysis regarding the quotations.  It allowed us to create the topic categories we think relevant for our analysis. To create such categories, we insert a few seed terms, wich are related words to the topic name. Those terms were manually picked using the Macmillan Thesaurus. Empath analysis returns the for a quote to be in a category, the most likely was defined as the main topic of the quote. Unfortunatly, many quotations were not labelled with a topic (around 70%). Indeed, many quotations are short and composed of words that are not direclty related to a specific topic like stopwords ('and','the'). Even when we manually read the quotation it was hard to specify a topic because it missed the context. We were pretty satisfied that the topic analysis shown us that most of Pope Francis quotations were related to religion and most of Donald Trump quotations were related to justice and politics, which seems coherent.

Considering now the speaker emitting the quote, we could not properly account for the differences in fame of all the speaker. Therefore, we filter only for quotes from famous people (as defined by the [Pantheon database](https://doi.org/10.7910/DVN/28201) to analyze what makes the fame of a quote. The Pantheon dataset was generated on the basis of Wikipedia bibliographies views, the number of different Wikipedia languages, the coefficient of variation etc. and it combines those values in a single metric, the historical popularity index (HPI). The HPI score will also be included as a feature to account for the remaining differences in speaker's fame. Moreover, this filtering step on famous speakers also allows to remove 'missense' quotes (not emitted by speakers, but rather text passages wrongly interpreted as a quote). We also considered some additional features about the speaker, its continent of origin, its occupation, its gender, and  whether he was alive at the date at which the quote wn nas emitted.

These generated new features allows us to complete our dataset and better characterize the quotes we are interested in, which we hope will help with supervised learning methods and downstream analysis.


### Supervised Learning
We wanted to try different supervised learning ML models on the dataset, like random forest, logistic regression and K-NN models to predict using the available features if a given quote is famous or not. The idea was to test different models and assess their performance using adequate metrics like accuracy, precision, and recall. You can find the methods and results in the M3 notebook.


### Unsupervised Learning
We tried different methods on unsupervised learning like k-NN or DBSCAN clustering, or KPrototypes for clustering with categorical and numerical features, or even KModes considering only categorical features. But the results weren't conclusive so we didn't continue trying to identify clusters in our data.

### Sentence embeddings
We generated embeddings of the quotes using the BERT model. This word representation allows detecting sentences that are closer in the embedding space and thus might reveal interesting patterns. Using PCA, we tried to visualize clustering by keeping 2 principal components. Unfortunalty we didn't observe any clustering between the famous and not famous quotes so we left the embeddings aside for the final analysis.

### Conclusion
There are some limitations of our analysis. First, we saw that most of the quotes we have are from North America so the results are a bit biased. Also, we didn't take into account the intonation or speech context which might play an important role in how a quote is portrayed in the press.

### Text generation
The last step of the project was to build a 'famous quote generator' that learns how to generate a 'famous' quote that we can use to be famous thanks to ADA. We selected a corpus of the 1000 most famous quotes across years, ranging from 98263 to 1028 occurrences. The text was preprocessed in order to remove punctuation and numbers as well as multiple spacing. An LSTM model was created and trained on 100 epoch using this corpus. The output of the model is the probability of the next word in the sequence. Once the model was trained, we generated new sentences using a random seed of 4 words and limiting its length to 13 words since it is the median length of famous quotes.

The sentences generated are not too bad considering the small dataset and the simplicity of our model. It successfully links ideas like 'terrorism' or 'murder' to 'horrible', 'victims' or 'resilience'. The syntax is a bit sketchy at times, but the grammatical order is usually respected. We still could generate some nice quotes such as:
"These murderous attacks have once again showed us the total hatred of humanity.” This one could definitely become a famous quote.

# Task
* Manon: preprocessing, supervised learning, univariate data analysis, plotting, website
* Pauline: speaker features, supervised learning, plotting, website
* Elodie: feature enrichment using NLP, generation of embeddings, quote generator, website
* Oihana: topic extraction, figures, notebook

# What did we learn?
We really enjoyed working on the project, which was fun and motivating till the end. We discovered a lot of different tools to play around with the dataset we had, and there are still some possibilities that we didn't explore.  We were a bit disappointed not to find some groundbreaking info about what makes a famous quote, but we guess that's what ADA is about. Anyway, it taught us an important lesson: it is not really the quote that makes you famous but what you make out of it.







