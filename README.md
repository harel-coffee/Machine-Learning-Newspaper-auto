Machine-Learning-Newspaper
======================

##**Step1. Data Wrangling**
- Run "data_wrangling.py"
- Get API Key from NYTimes.
- Get articles from NYTimes and convert json to csv format to save.
- They don't provide full article.
- Challenges:
 * simplejson library errors occurs and fixed it with upgrade 3.6.5.
 * Sometimes server timeout.
 * Article have utf-8 and unicode both of them.
 * Sometimes JSON Data contains journalist name but does not have article.
  
 
##**Step2. Data Exploratory**
- Run "data_exploratory.py"
- Clean stemmer with SnowballStemmer.
- Change encoding utf-8 to unicode.
- step2_data_exploratory.py generates pkl file with all article from 2010 to 2014.
 * It is to expensive to my MAC.
- step2_data_exploratory(2_people).py generates pkl file with two journalist's articles from 2010 to 2014.
 * It is not that expensive.
 * I choose two journalist, NEIL GENZLINGER and STEPHEN HOLDEN because they have written so many articles.
 * During 2010~2014, NEIL GENZLINGER wrote 1211 articles and STEPHEN HOLDEN wrote 1317 articles.
 

##**Step3. Feature Engineering**
- Feature Extraction
 * Applied TfidfVectorizer and deleted stopwords.
- Feature Selection
 * SelectKBest, chi2 are faster than SelectPercentile in my case.
 * f_classif for classification problem.
 * f_regression for regression problems.
 * chi2 for classification problems with sparse non-negative data (typically text data).
 * My prefer : SelectPercentile(score_func=chi2), SelectKBest(k=100), SelectPercentile(f_classif, percentile=30).
- preprocess_4 method is for supervised learning.
- preprocess_2 method is for unsupervised learning.


##**Step4. Apply Different Algorithm**
- I applied various Supervised and Unsupervised Algorithm with Dimension Reduction.
- Supervised Learning
 * Classification : GaussianNB, BernoulliNB, AdaBoostClassifier, DecisionTreeClassifier, KNeighborsClassifier, RandomForestClassifier, SVC
 * Regression : LinearRegression, ElasticNet, Lasso, Ridge
- Unsupervised Learning
 * KMeans, SpectralClustering, AgglomerativeClustering
- Dimension Reduction
 * Linear Dimensionality Reduction : PCA(supervised), RandomizedPCA(supervised), LDA(unsupervised)
 * Non Linear Dimensionality Reduction : Isomap(unsupervised), LocallyLinearEmbedding(unsupervised)
 
 
 Algorithm | Feature Selection | Accuracy | Time |
 ----------|--------------------|----------|----------|
 GaussianNB |  SelectPercentile | 0.93 | 0.3s|
 GaussianNB | chi2 | 0.93 | 0.12s|
 BernoulliNB | SelectPercentile | 0.92 | 0.2s|
 BernoulliNB | chi2 | 0.90 | 0.06s|
 AdaBoostClassifier | SelectPercentile | 0.72 | 14s|
 AdaBoostClassifier | chi2 | 0.71 | 4.6s|
 DecisionTreeClassifier | SelectPercentile | 0.79 | 9s|
 DecisionTreeClassifier | chi2 | 0.80 | 2.2s|
 KNeighborsClassifier | SelectPercentile | 0.75 | 3s|
 KNeighborsClassifier | chi2 | 0.55 | 1.0s|
 RandomForestClassifier | SelectPercentile | 0.84 | 2s|
 RandomForestClassifier | chi2 | 0.85 | 0.8s|
 RandomForestClassifier | SelectPercentile | 0.88 | 30s|
 RandomForestClassifier | chi2 | 0.87 | 10s|


Feature Selection : SelectKBest
<img src="https://app.box.com/s/n9gndwsaqgzh39b61vlzwamslvclb2kv" />


Feature Selection : SelectPercentile
<img src="http://bokeh.pydata.org/en/latest/_images/histogram_t.png" />


 Algorithm | Feature Selection | Accuracy | Time |
 ----------|--------------------|----------|----------|
 KMeans |  SelectPercentile(50) | 0.59 | 3.0s|
 KMeans |  chi2 | 0.44 | 0.6s|
 KMeans |  SelectKBest(300) | 0.47 | 0.1s|
 SpectralClustering |  SelectPercentile(50) | 0.52 | 2.7s|
 SpectralClustering |  chi2 | 0.47 | 2.1s|
 SpectralClustering |  SelectKBest(300) | 0.47 | 2.2s| 
 AgglomerativeClustering(n_clusters=2, linkage='ward') |  chi2 | 0.63 | 36.3s|
 AgglomerativeClustering(n_clusters=2, linkage='ward') |  SelectKBest(300) | 0.49 | 21.4s| 
 AgglomerativeClustering(n_clusters=2, linkage='ward') |  chi2 | 0.49 | 18.9|
 AgglomerativeClustering(n_clusters=2, linkage='complete') |  SelectKBest(300) | 0.47 | 36.1s| 
 AgglomerativeClustering(n_clusters=2, linkage='complete') |  chi2 | 0.51 | 22.4s|
 AgglomerativeClustering(n_clusters=2, linkage='complete') |  SelectKBest(300) | 0.48 | 18.5s|
 AgglomerativeClustering(n_clusters=2, linkage='average') |  SelectKBest(300) | 0.47 | 36.4s| 
 AgglomerativeClustering(n_clusters=2, linkage='average') |  chi2 | 0.47 | 20.4s|
 AgglomerativeClustering(n_clusters=2, linkage='average') |  SelectKBest(300) | 0.47 | 18.7s|
 
 
 Feature Selection : SelectKBest
<img src="http://bokeh.pydata.org/en/latest/_images/histogram_t.png" />


Feature Selection : SelectPercentile
<img src="http://bokeh.pydata.org/en/latest/_images/histogram_t.png" />


 Algorithm | Time | Opinion | 
 ----------|--------------------|----------|
 PCA |  16s | 70 features and graph looks stable |
 RandomizedPCA | 0.7s | 80 features and graph looks unstable|
 LDA | 16s | graph looks stable |
 Isomap | 73s | 0.90 |
 LocallyLinearEmbedding | 45s | 0.72 |
 
 
 Dimension Reduction : PCA
 <img src="http://bokeh.pydata.org/en/latest/_images/histogram_t.png" />


 Dimension Reduction : RandomizedPCA
 <img src="http://bokeh.pydata.org/en/latest/_images/histogram_t.png" />


 Dimension Reduction : LDA
 <img src="http://bokeh.pydata.org/en/latest/_images/histogram_t.png" />


 Dimension Reduction : Isomap
 <img src="http://bokeh.pydata.org/en/latest/_images/histogram_t.png" />


 Dimension Reduction : LocallyLinearEmbedding
 <img src="http://bokeh.pydata.org/en/latest/_images/histogram_t.png" />


 