# ADA made me famous!

## Abstract
### “Shoot for the moon. Even if you miss, you'll land among the stars.” Norman Vincent Peale
Did you ever dream of your words like the ones of Shakespeare, Einstein or Trump remaining forever etched in the memory of humanity?  Would you like to be famous? Then this project might help you!
We decided to explore what makes a famous quote. Is it its length? Its topic? Or something only a proper EDA could reveal? The idea is to study a maximum number of features of quotes evaluated as ‘famous’ in order to try to characterize the perfect quote. Maybe this study will reveal some hidden patterns about them. Combined with ML and NLP, we could create a perfect quote generator and try to become famous thanks to ADA!


## Research questions and ideas
The aim of our project is to try to characterize what makes a quote famous. To do so we have different ideas to explore and enrich the dataset we have, in order to design a more complete analysis.

- We want to be able to define the topic of a quote using NLP or by looking at the journals they were published in (based on the URL), and analyze what was the hot-topic of each year (eg. 2016 presidential, 2020 health etc.).
* Using NLP methods we want to enrich the quote features by assessing their positivity and subjectivity, as well as quantifying their language complexity.
- Explore the link between the most quoted sentences and their speaker. For instance trying to determine the impact of the fame of the speaker on the number of occurrences of a quote.
- Maybe define a fame score for our data based on the number of occurrences, the speaker and the journal where it was published? This could refine the analysis instead of having a binary outcome ‘famous’ or ‘non-famous’, quantifying fame is one of the challenge of this project.
- Test if we are able to build a model that is able to predict whether a quote will be famous or not. The idea is to train the model  on a random subset across all years and then test it on an unused validation subset.
The end goal is to unravel some pattern shared across “famous” quotes, for example the theme or vocabulary (formal, etc.)  of a quote, and then build a model that generates the “ideal” quotes.
- Keep a critical eye on our project to have knowledge on its limitations and avoid misleading informations.

## Methods
### Preprocessing and filtering
The first step of the project is to preprocess the data in order to have an exploitable and trustworthy dataset. Our main criterion to define what is a famous quote is the number of occurrences associated with it. When analyzing the distribution of the number of occurrences across the different years, we observed that most of the quotes (75%) have been quoted only once or twice. Since we want to focus on only famous quotes, we decided to filter on the 99.9th percentile, keeping only the quotes with the highest number of occurrences (above 215) and label them as famous (encoded by 1 in the’ famous’ column). In order to be able to compare and contrast with ‘non-famous’ quotes (encoded by 0 in the ‘famous’ columns), we  took a sample of quotes which appeared less than 10 times throughout the different years. Thus, we have a total of 257 378 quotes, with 115 218 famous quotes and 142 160 non-famous quotes

We decided to remove quotes where the speaker is attributed to 'None' with the highest probability. Indeed, we observed that the second speaker often has a very low probability, so an analysis of fame based on attributes of the speaker seems irrelevant. Moreover, when looking at the citations associated with 'None' speakers, they seem like text pages and not real quotes.This brings the dataset down to 68 355 famous quotes and 93 149 non-famous quotes. More covariates were added like the lengths of a quote (number of words) and the number of characters. We retrieved the speaker’s attribute using the Wikidata entities in the speaker_attributes.parquet file in order to study how these covariates impact our research question.

### Exploratory Data Analysis
Once the dataset filtered and extended, we started to perform an univariate data analysis with summary statistics and graphical information on distribution of each covariate in order to get a better understanding of the data and design a more complex data analysis.

Then, multivariate data analysis will follow to understand the relation between the different covariates associated with a quote. We will use scatterplots in order to understand the correlation between the different variables and linear regression to have a more complete insight on their relation.

### Supervised Learning
We wanted to try different supervised learning ML models on the dataset, like random forest, CNN or logistic regression in order to predict using the features available if a given quote is famous or not. The idea would be to test different models and assess their performance using adequate metrics like accuracy or F1 score for instance. Before training our models on the dataset, we wanted to explore how to enrich the features with more covariates since some models perform better with more variables.

Libraries to use: Sklearn (random forest and logistic regression), Keras (CNN)

### Dataset enrichment
In order to enrich our dataset with new features, we need to compute them using available methods. Some NLP methods allow us to extract for instance the polarity and subjectivity of a quote, that is to say it’s sentiment. This can be achieved using the Textblob library. Another characterization that might be interesting is the lexical richness and lexical readability, which try to measure the complexity of a sentence. It allows us to generate new features to complete our dataset and better characterize the quotes we are interested in.

We also want to try to retrieve the topic of a quote in order to see if a specific theme is more plebiscite than others. The most promising way to do so is by using topic modelling. The most popular topic modelling technique is called LDA which allows you to retrieve hidden themes in a text. It’s an unsupervised learning method that can be implemented in python.

Libraries to use: TextBlob (polarity and subjectivity), nltk and gensim(topic extraction)

### Sentence embeddings
We could use some state-of-the-art natural language processing methods and generate embeddings of the quotes using BERT or ELMo models. This word representation allows us to detect sentences that are closer in the embedding space and thus reveal interesting patterns. Using PCA, we could try to visualize clustering by keeping 2 principal components. Cosine distance between quotes could be computed in order to determine their proximity in the embedding space. Embeddings and clustering could hence be used for unsupervised machine learning methods.

Libraries to use: sentence_transformer (embeddings), sklearn (PCA)


### Text generation
The last idea we have for the project would be to generate a new quote based on the corpus of famous quotes we have using LSTMs. Generation of text can be implemented using deep learning models and would be a fun way to conclude our project.

Libraries to use: Tensorflow

# Timeline
![TIMELINE.jpg](https://github.com/epfl-ada/ada-2021-project-aficionada/blob/main/TIMELINE.jpg?raw=true)

# Question for TAs
- Would there be a way to obtain the lifetime of a quote (first and last emission date) ? We were also wondering if there would be an efficient way to run through all years and see if one “famous” or “non-famous” quote is present in different datasets/years ?
Indeed, it would be interesting to distinguish quotes that make the buzz at a given time point from an everlasting quote across generations. 
- Is there a way to assess when a person became famous, if it is before the emission date of the quote ? Is there a way to group occupations together ?








