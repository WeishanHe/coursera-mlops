# Select and Train a Model
## Selecting and Training a Model
#### Modeling overview
- model-centric AI development vs. Data-centric AI development 
-  Data-centric AI development is useful in practical case. It is more than collecting more data. Use tools to improve the data in the most efficient possible way.
#### Key challenges
- AI system  = Code (algorithm/model) + Data
![model centric](images\model_centric.png)
- challenges in model development
	1. Doing well on training set (usually measured by average training error)
	2. Doing well on dev/test sets
	3. Doing well on business metrics/project goals
#### Why low average error isn't good enough
- Performance on disproportionately important examples
- Performance on key slices of the dataset
	- ex: ML for loan approval - make sure not to discriminate by ethnicity, gender, location, language or other procteded attributes
	- ex: Product recommendations from retailers - Be careful to treat fairly all major user, retailer, and product categories
- Rare classes
	- skewed data distribution
	- accuracy in rare classes
#### Establish a baseline
![establish baseline](images\establish_baseline.png)
- Ways to establish a baseline
	- Human level performance (HLP)
	- Literature search for state-of-the-art/open
	- Quick-and-dirty implementation
	- Performance of older system
- Baseline helps to indicates what might be possible. In some cases (such as HLP) is also gives a sense of what is irreducible error/Bayes error.
#### Tips for getting 
- Getting started on modeling
	- Literature search to see what's possible (course, blogs, open-source projects)
	- Find open-source implementations if available
	- A reasonable algorithm with good data will often outperform a great algorithm with no so good data
- Should you take into account deployment constraints when picking a model?
	- Yes, if baseline is already established and goal is to build and deploy. 
	- No (or not necessarily), if the purpose is to establish a baseline and determine what is possible and might be worth pursuing
- Sanity-check for code and algorithm
	- Try to overfit a small training dataset before training on a large one
## Error analysis and performance auditing
#### Error analysis example
- it is a iterative process
- use tags to slice your data. The tags don't have to be mutually exlucsive.
- useful metrics for each tag
	- What fraction of errors has that tag?
	- Of all data with that tag, what fraction is misclassified?
	- What fraction of all the data has that tag?
	- How much room for improvement is there on data with that tag?
#### Prioritizing what to work on
![prioritizing](images\prioritizing.png)
- decide on most important categories to work on based on:
	- How much room for improvement there is
	- How frequently that category appears
	- How easy is to improve accuracy in that category
	- How important it is to improve in that category
- Adding/improving data for specific categories
	 For categories you want to prioritize
	 - Collect more data
	 - Use data augmentation to get more data
	 - Improve label accuracy/data quality
#### Skewed datasets
When it comes to detecting rare cases, the accuracy will be really high even if the algorithm failed to detect a lot of these cases. That is the reason why we use F1 score.
- Confusion matrix: Precision and Recall
![confusion matrix](images\confusion_matrix.png)
- Combining precision and recall - F1 score (harmonious mean of precision and recall)
![f1 score](images\f1_score.png)
- Multi-class metrics
manufacturing cares more about the recall since they don't want defected products go into market
![multiclass metrics](images\multiclass_metrics.png)

#### Performance auditing
- Auditing framework
	- Check for accuracy, fairness/bias, and other problems
		1. Brainstorm the ways the system might go wrong
			- Performance on subsets of data (e.g., ethnicity, gender)
			- How common are certain errors (e.g., FP, FN)
			- Performance on rare cases
		2. Establish metrics to assess performance against these issues on appropriate slices of data
		3. Get business/product owner buy-in
## Data iteration
#### Data-centric AI development
- model-centric view: take the data you have and develop a model that does as well as possible on it. In other words, we hold the data fixed and iteratively improve the code/model.
- data-centric view: The qualify of the data is paramount. Use tools to improve the data quality; this will allow multiple models to do well. We hold the code fixed and iteratively improve the data.
#### A useful picture of data augmentation
![data augmentation](images\data_augmentation.png)
- classify the noise
- benchmark model performance against HLP
- use error analysis to determine which segment to augment data. It turns out that if performance on cafe noise goes up, probably performance on the nearby points will go up too and performance on far-away points may or may not go up as much. 
- The biggest gap shifts and error analysis will help you find the next most valuable point to improve.
#### Data augmentation
- Goal: Create realistic examples that (i) the algorithm does poorly on, but (ii) humans (or other baseline) do well on.
- Checklist:
	- Does it sound realistic? (i)
	- Is the x $\rightarrow$ y mapping clear? (e.g., can humans recognize speech?)(ii)
	- Is the algorithm currently doing poorly on it?
![data-centric](images\data_centric.png)

#### Can adding data hurt?
- Where does this question come from: augmenting data can change the distribution of the data.
- For unstructured data problems, if:
	- The model is large (low bias)
	- The mapping x $\rightarrow$ y is clear (e.g., given only the input x, humans can make accurate predictions) (1 vs. I)
	Then, adding data rarely hurts accuracy.
#### Adding features
![restaurant recommendation](images\restaurant_recom.png)
- Product recommendation is shifting from collaborative filtering to content based filtering
	- collaborative filtering: looks at the user and try to figure out who is similar to that user and then recommend things to you that people like you also like.
	- content based filtering: look at you as a person and look at the description of the restaurant or look at the menu of the restaurants and look at other information about the restaurant, to see if that restaurant is a good match for you or not. The advantage of content based filtering is that even if there's a new restaurant or a new product that hardly anyone else has liked, by looking at the description of the restaurant, rather than just looking at who else like the restaurants, you can more quickly make good recommendations (cold-start problem). 
- Data iteration
	- Error analysis can be harder if there is no good baseline (such as HLP) to compare to
	- Error analysis, user feedback and benchmarking to competitors can all provide inspiration for features to add
#### Experiment tracking
- What to track:
	- Algorithm/code versioning
	- Dataset used
	- Hyperparameters
	- Save the results
- Tracking tools
	- Text files
	- Spreadsheet
	- Experiment tracking system: Comet, MLflow, Sage Maker Studio, LandingAI
- Desirable features
	- Information needed to replicate results
	- Experiment results, ideally with summary metrics/analysis
	- Perhaps also: resource monitoring, visualization, model error analysis
#### From big data to good data
Try to ensure consistently high-quality data in all phases of the ML project lifecycle
- Good data
	- Covers important cases (good coverage of inputs x)
	- Is defined consistently (definition of labels y is unambiguous)
	- Has timely feedback from production data (distribution covers data drift and concept drift)
	- Is sized appropriately
## Week 2 Optional References
**Week 2: Select and Train Model**

If you wish to dive more deeply into the topics covered this week, feel free to check out these optional references. You won’t have to read these to complete this week’s practice quizzes. [Establishing a baseline](https://blog.ml.cmu.edu/2020/08/31/3-baselines/)

[Error analysis](https://techcommunity.microsoft.com/t5/azure-ai/responsible-machine-learning-with-error-analysis/ba-p/2141774)

[Experiment tracking](https://neptune.ai/blog/ml-experiment-tracking)

**Papers**

Brundage, M., Avin, S., Wang, J., Belfield, H., Krueger, G., Hadfield, G., … Anderljung, M. (n.d.). Toward trustworthy AI development: Mechanisms for supporting verifiable claims∗. Retrieved May 7, 2021[http://arxiv.org/abs/2004.07213v2](http://arxiv.org/abs/2004.07213v2)

Nakkiran, P., Kaplun, G., Bansal, Y., Yang, T., Barak, B., & Sutskever, I. (2019). Deep double descent: Where bigger models and more data hurt. Retrieved from [http://arxiv.org/abs/1912.02292](http://arxiv.org/abs/1912.02292)

