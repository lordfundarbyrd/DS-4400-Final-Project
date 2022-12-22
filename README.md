# DS-4400-Final-Project

**Predicting Counter Strike Round Winners**

**Abstract**

Whether or not a team wins a game of Counter Strike: Global Offensive, is a product of a team&#39;s strategy and skill. However, it also involves a variety of other factors that a cursory analysis might not be able to catch. We propose using a variety of models, including logistic regression, support vector machines, and k-nearest neighbors, to classify which team will win a given round based on a variety of features in our dataset. The most accurate model, if reasonably accurate, could substantially improve the likelihood of successful bets in the nascent-but-growing esports betting scene, change what strategies teams use to win, or alter how commentators approach their work.

**Introduction**

In the game of Counter Strike: Global Offensive, two teams, the Terrorists and Counter-Terrorists, fight to win a round. There are different win conditions depending on the team. If every member on a team is killed, the other team wins the round. Otherwise, if the Terrorists are successfully able to plant a bomb and keep the Counter-Terrorists from defusing it, then they win the match. If the Counter-Terrorists defuse the bomb successfully, then they win the match.

There are many variables that influence a team&#39;s success in a round, such as the map on which the round takes place, the money players have on hand, which is used to buy guns and supplies like helmets (which reduce damage taken), and health and armor points of all players. While strategy is also key in the game, the objective measurements previously mentioned can be an indicator of which team is going to win or lose. Thus, we will be attempting to classify each team as the round-winner or not, for each round of the match. Given the multi-billion dollar esports industry and the similarity of the structure of various video games, this model could be expanded to multiple other video games such as Valorant, a first-person shooter which shares many mechanics with Counter Strike, and League of Legends, a different team-based game that nevertheless has many round-influencing features. Thus, casters and commentators could use this model to give a preview of the current round. Additionally, the esports betting scene and sites such as gg.bet could also take advantage of this model, influencing which team to bet on.

**Technical Approach**

We decided to run multiple different types of classification models on our dataset in order to predict the winner of each round. We used Naive Bayes, logistic regression, K-Neighbors Regressor, Linear SVC, and Linear SVM with linear, polynomial kernels, sigmoid, and radial basis function kernels. Our dataset was mostly already cleaned and prepared, but before putting our data through the various models, we used LabelEncoder to convert our categorical data into quantitative data, and then used a standard scalar to remove the mean and scale to unit variance. We split the data into training and testing sets. We then compared the accuracy and error for each model we used, along with other classification metrics such as precision, recall, and f1 scores. We then used Recursive Feature Selection and to see which features were the best to use. We also use GridSearchCV to fine tune hyperparameters and use cross validation to improve model performance.

**Experimental Results**

We found our dataset on Kaggle, which contains data on CS:GO rounds at various time points. The dataset contains 96 features, such as the health and armor points of players, whether or not the bomb has been set by the Terrorists, how many players are still alive, and how many of each weapon is in use, all indexed to 20-second time intervals, recorded as the amount of time remaining in that round (each round lasts 180 seconds) . All data points should be considered independent of each other. Many of these features exist for both Terrorists and Counter-Terrorists. The features we wish to use are already in our dataset so feature extraction was not necessary. Our dataset contains 122410 samples, 62406 of which are rounds where Terrorists won, and 60004 of which are rounds where Counter-Terrorists won, which is reasonably balanced. For this dataset, we decided to run various regression and classification models to determine whether Terrorists or Counter-Terrorists won a specific round based on various features and to see which model(s) performed best.

For training of all models, we used scikit-learn&#39;s implementation (train\_test\_spit). Our data was split into 75% training and 25% testing. Our target was &quot;round\_winner&quot;, while our features consisted of the rest of the columns. We then ran our models and calculated the accuracy, precision score, recall score, and F1 score for each model for both our training and testing sets.

All 4 models seemed to perform at relatively the same level, with ~75% classification accuracy on training and testing sets. For the training sets, the support vector machine with a polynomial kernel performed best with 81.7% classification accuracy, and the support vector machine with a sigmoid kernel performed worst with a 68% classification accuracy. For the testing sets, the support vector machine with polynomial kernel again performed the best with a classification accuracy of 78.9%. The support vector machine with a sigmoid kernel again performed the worst with a classification accuracy of 68%.

Training Set

| Name | Accuracy Score | Precision Score | Recall Score | F1 Score |
| --- | --- | --- | --- | --- |
| K-Neighbors | 74.8% | .78 | .70 | .74 |
| Logistic Regression | 74.9% | .76 | .74 | .75 |
| Linear Support Vector Machine | 75.02% | .76 | .74 | .75 |
| SVC - polynomial kernel | 81.7% | .85 | .77 | .81 |
| SVC - radial basis function kernel | 81.07% | .85 | .76 | .8 |
| SVC - sigmoid kernel | 68% | .687 | .685 | .686 |
| SVC - linear kernel | 75.22% | .78 | .7 | .74 |
| Naive Bayes | 69.5% | .79 | .55 | .64 |

Testing Set

| Name | Accuracy Score | Precision Score | Recall Score | F1 Score |
| --- | --- | --- | --- | --- |
| K-Neighbors | 74.5% | .77 | .70 | .738 |
| Logistic Regression | 74.9% | .75 | .74 | .75 |
| Linear Support Vector Machine | 74.9% | .76 | .74 | .75 |
| SVC - polynomial kernel | 78.9% | .822 | .749 | .78 |
| SVC - radial basis function kernel | 78.5% | .822 | .738 | .77 |
| SVC - sigmoid kernel | 68% | .69 | .687 | .68 |
| SVC - linear kernel | 75.2% | .78 | .71 | .74 |
| Naive Bayes | 69.4% | .78 | .545 | .64 |

Next, we saw that the best hyperparameters for logistic regression were to use the L2 penalty, as well as with a regularization coefficient of .001, with an average cross validation score of 74.9% on the training data and 75% on the testing data, a .01% increase for testing data accuracy.

From recursive feature selection, we found that the top 5 best features were time left, ct\_armor, t\_armor, ct\_money, and t\_money. Using these best features, we then used a heatmap to visualize the correlation between these features, and plotted the most correlated features against each other.

<img width="496" alt="image" src="https://user-images.githubusercontent.com/15839864/209045422-ab64b066-3932-453a-8163-f01fec7487d0.png"> <img width="496" alt="image" src="https://user-images.githubusercontent.com/15839864/209045472-44838128-779b-4eaf-b8fc-19c947c79fc7.png">

<img width="496" alt="image" src="https://user-images.githubusercontent.com/15839864/209045560-10376e4f-95d6-424c-b041-ca62a9026ab0.png"> <img width="496" alt="image" src="https://user-images.githubusercontent.com/15839864/209045590-4a3f1060-7bab-48aa-8987-f65efaa4515c.png">

<img width="496" alt="image" src="https://user-images.githubusercontent.com/15839864/209045746-b5db4693-161c-4e20-987d-99ad932ff79f.png"> <img width="496" alt="image" src="https://user-images.githubusercontent.com/15839864/209045786-134cc87c-77bc-4cd0-b938-9431e394fed1.png">

**References**

Dataset: [https://www.kaggle.com/christianlillelund/csgo-round-winner-classification](https://www.kaggle.com/christianlillelund/csgo-round-winner-classification)

Documentation used:

- [https://seaborn.pydata.org/generated/seaborn.heatmap.html](https://seaborn.pydata.org/generated/seaborn.heatmap.html)
- [https://matplotlib.org/stable/api/\_as\_gen/matplotlib.pyplot.scatter.html](https://matplotlib.org/stable/api/_as_gen/matplotlib.pyplot.scatter.html)
