Introduction to Data Mining
====================================

DATA MINING

Data Mining
Data Mining is an analytic process designed to explore data (usually large amounts of data - typically business or market related) in search of consistent patterns and/or systematic relationships between variables, and then to validate the findings by applying the detected patterns to new subsets of data. The ultimate goal of data mining is prediction - and predictive data mining is the most common type of data mining and one that has the most direct business applications. The process of data mining consists of three stages: (1) the initial exploration, (2) model building or pattern identification withvalidation/verification, and (3) deployment (i.e., the application of the model to new data in order to generate predictions).



















Stage 1: Exploration. This stage usually starts with data preparation which may involve cleaning data, data transformations, selecting subsets of records and - in case of data sets with large numbers of variables ("fields") - performing some preliminary feature selection operations to bring the number of variables to a manageable range (depending on the statistical methods which are being considered). Then, depending on the nature of the analytic problem, this first stage of the process of data mining may involve anywhere between a simple choice of straightforward predictors for a regression model, to elaborate exploratory analyses using a wide variety of graphical and statistical methods (see Exploratory Data Analysis (EDA)) in order to identify the most relevant variables and determine the complexity and/or the general nature of models that can be taken into account in the next stage.

Stage 2: Model building and validation. This stage involves considering various models and choosing the best one based on their predictive performance (i.e., explaining the variability in question and producing stable results across samples). This may sound like a simple operation, but in fact, it sometimes involves a very elaborate process. There are a variety of techniques developed to achieve that goal - many of which are based on so-called "competitive evaluation of models," that is, applying different models to the same data set and then comparing their performance to choose the best. These techniques - which are often considered the core of predictive data mining - include: Bagging (Voting, Averaging), Boosting, Stacking (Stacked Generalizations), and Meta-Learning.

Stage 3: Deployment. That final stage involves using the model selected as best in the previous stage and applying it to new data in order to generate predictions or estimates of the expected outcome.

The concept of Data Mining is becoming increasingly popular as a business information management tool where it is expected to reveal knowledge structures that can guide decisions in conditions of limited certainty. Recently, there has been increased interest in developing new analytic techniques specifically designed to address the issues relevant to business Data Mining (e.g., Classification Trees), but Data Mining is still based on the conceptual principles of statistics including the traditional Exploratory Data Analysis (EDA) and modeling and it shares with them both some components of its general approaches and specific techniques.

However, an important general difference in the focus and purpose between Data Mining and the traditional Exploratory Data Analysis (EDA) is that Data Mining is more oriented towards applications than the basic nature of the underlying phenomena. In other words, Data Mining is relatively less concerned with identifying the specific relations between the involved variables. For example, uncovering the nature of the underlying functions or the specific types of interactive, multivariate dependencies between variables are not the main goal of Data Mining. Instead, the focus is on producing a solution that can generate useful predictions. Therefore, Data Mining accepts among others a "black box" approach to data exploration or knowledge discovery and uses not only the traditional Exploratory Data Analysis (EDA) techniques, but also such techniques as Neural Networks which can generate valid predictions but are not capable of identifying the specific nature of the interrelations between the variables on which the predictions are based.

Data Mining is often considered to be "a blend of statistics, AI (artificial intelligence), and data base research" (Pregibon, 1997, p. 8), which until very recently was not commonly recognized as a field of interest for statisticians, and was even considered by some "a dirty word in Statistics" (Pregibon, 1997, p. 8). Due to its applied importance, however, the field emerges as a rapidly growing and major area (also in statistics) where important theoretical advances are being made (see, for example, the recent annual International Conferences on Knowledge Discovery and Data Mining, co-hosted by the American Statistical Association).

For information on Data Mining techniques, review the summary topics included below. There are numerous books that review the theory and practice of data mining; the following books offer a representative sample of recent general books on data mining, representing a variety of approaches and perspectives: 

Berry, M., J., A., & Linoff, G., S., (2000). Mastering data mining. New York: Wiley.

Edelstein, H., A. (1999). Introduction to data mining and knowledge discovery (3rd ed). Potomac, MD: Two Crows Corp.

Fayyad, U. M., Piatetsky-Shapiro, G., Smyth, P., & Uthurusamy, R. (1996). Advances in knowledge discovery & data mining. Cambridge, MA: MIT Press.

Han, J., Kamber, M. (2000). Data mining: Concepts and Techniques. New York: Morgan-Kaufman.

Hastie, T., Tibshirani, R., & Friedman, J. H. (2001). The elements of statistical learning : Data mining, inference, and prediction. New York: Springer.

Pregibon, D. (1997). Data Mining. Statistical Computing and Graphics, 7, 8. 

Weiss, S. M., & Indurkhya, N. (1997). Predictive data mining: A practical guide. New York: Morgan-Kaufman.

Westphal, C., Blaxton, T. (1998). Data mining solutions. New York: Wiley.

Witten, I. H., & Frank, E. (2000). Data mining. New York: Morgan-Kaufmann.



### Broad and Narrow Definitions
 
- Broad definition includes traditional statistical techniques
- Narrow definition emphasizes automated and heuristic methods
- Key concepts in Data Mining Include : data dredging , fishing expeditions
- Key paper: Knowledge Discovery in Databases (Usama Fayyad)

### What is Data Mining
- First Workshop on Data Mining KDD was in 1995
- Recently coined terms for confluence of ideas from statistics and computers science (Machine Learning and Database Methods) applied to 
large databases in science, engineering and business
- In a state of flux, many definitions, lots of debate about what it is and what it is not.
- Terminology is not standard (e.g. bias classification, prediction, features (independent variables)
target (dependent variables), case (explempar, row)
- "Statistics at Scale and Speed (with Simplicity) - Darryl Pregibon
- 
### Illustrative Examples
- Customer Relationship Managment (Target MArketing, Attrition Predicton/Churn Analysis,Fraud Detection, Credit Scoring)
- Finance  (Business problem/solution approach)
- E-commerce and Internet (Collaborative Filtering/ From Clicks to Customers)
- 
<hr>
### Recommendation Systems
- Business Opportunity: Users rate items (Amazon.com etc on the web) how to use recommendations for other users to infer ratings for a particular user.
- Solution: Use of a Technique known as ***collaborative filtering***
- Benefit : Increased Revenue by Cross Selling, Up Selling


### Emerging Major Data Mining Applications
- SPam filtering
- Bioinformatics/Genomics
- Medical History Data - Insurance Claims
- Personalization of servies in e-commerce
- RF tags (gillette)
- Security 
 - Container Shipments
 - Network Intrusion Systems
