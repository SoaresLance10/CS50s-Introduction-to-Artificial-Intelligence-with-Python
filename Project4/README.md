# Nim and Shopping
## Shopping
Write an AI to predict whether online shopping customers will complete a purchase.

When users are shopping online, not all will end up purchasing something. Most visitors to an online shopping website, in fact, likely don’t end up going through with a purchase during that web browsing session. It might be useful, though, for a shopping website to be able to predict whether a user intends to make a purchase or not: perhaps displaying different content to the user, like showing the user a discount offer if the website believes the user isn’t planning to complete the purchase. How could a website determine a user’s purchasing intent? That’s where machine learning will come in.

Your task in this problem is to build a nearest-neighbor classifier to solve this problem. Given information about a user — how many pages they’ve visited, whether they’re shopping on a weekend, what web browser they’re using, etc. — your classifier will predict whether or not the user will make a purchase. Your classifier won’t be perfectly accurate — perfectly modeling human behavior is a task well beyond the scope of this class — but it should be better than guessing randomly. To train your classifier, we’ll provide you with some data from a shopping website from about 12,000 users sessions.

The **specifications** for the project as mentioned at: https://cs50.harvard.edu/ai/2020/projects/4/shopping/
### Specification

Complete the implementation of **load_data**, **train_model**, and **evaluate** in shopping.py.

The **load_data** function should accept a CSV filename as its argument, open that file, and return a tuple (evidence, labels). evidence should be a list of all of the evidence for each of the data points, and labels should be a list of all of the labels for each data point.

•	Since you’ll have one piece of evidence and one label for each row of the spreadsheet, the length of the evidence list and the length of the labels list should ultimately be equal to the number of rows in the CSV spreadsheet (excluding the header row). The lists should be ordered according to the order the users appear in the spreadsheet. That is to say, evidence[0] should be the evidence for the first user, and labels[0] should be the label for the first user.

•	Each element in the evidence list should itself be a list. The list should be of length 17: the number of columns in the spreadsheet excluding the final column (the label column).

•	The values in each evidence list should be in the same order as the columns that appear in the evidence spreadsheet. You may assume that the order of columns in shopping.csv will always be presented in that order.

•	Note that, to build a nearest-neighbor classifier, all of our data needs to be numeric. Be sure that your values have the following types:
1. Administrative, Informational, ProductRelated, Month, OperatingSystems, Browser, Region, TrafficType, VisitorType, and Weekend should all be of type int
2. Administrative_Duration, Informational_Duration, ProductRelated_Duration, BounceRates, ExitRates, PageValues, and SpecialDay should all be of type float.
3. Month should be 0 for January, 1 for February, 2 for March, etc. up to 11 for December.
4. VisitorType should be 1 for returning visitors and 0 for non-returning visitors.
5. Weekend should be 1 if the user visited on a weekend and 0 otherwise.

•	Each value of labels should either be the integer 1, if the user did go through with a purchase, or 0 otherwise.

•	For example, the value of the first evidence list should be [0, 0.0, 0, 0.0, 1, 0.0, 0.2, 0.2, 0.0, 0.0, 1, 1, 1, 1, 1, 1, 0] and the value of the first label should be 0.

The **train_model** function should accept a list of evidence and a list of labels, and return a scikit-learn nearest-neighbor classifier (a k-nearest-neighbor classifier where k = 1) fitted on that training data.

•	Notice that we’ve already imported for you from sklearn.neighbors import KNeighborsClassifier. You’ll want to use a KNeighborsClassifier in this function.

The **evaluate** function should accept a list of labels (the true labels for the users in the testing set) and a list of predictions (the labels predicted by your classifier), and return two floating-point values (sensitivity, specificity).

•	**sensitivity** should be a floating-point value from 0 to 1 representing the “true positive rate”: the proportion of actual positive labels that were accurately identified.

•	**specificity** should be a floating-point value from 0 to 1 representing the “true negative rate”: the proportion of actual negative labels that were accurately identified.

•	You may assume each label will be 1 for positive results (users who did go through with a purchase) or 0 for negative results (users who did not go through with a purchase).

•	You may assume that the list of true labels will contain at least one positive label and at least one negative label.


A video Demonstrating the Functionality of this Project and be found at: https://youtu.be/EON86cH5zFA

# Nim
Write an AI that teaches itself to play Nim through reinforcement learning.

The **specifications** for the project as mentioned at: https://cs50.harvard.edu/ai/2020/projects/4/nim/
### Specification

Complete the implementation of **get_q_value**, **update_q_value**, **best_future_reward**, and **choose_action** in nim.py. For each of these functions, any time a function accepts a state as input, you may assume it is a list of integers. Any time a function accepts an action as input, you may assume it is an integer pair (i, j) of a pile i and a number of objects j.

The **get_q_value** function should accept as input a state and action and return the corresponding Q-value for that state/action pair.

•	Recall that Q-values are stored in the dictionary self.q. The keys of self.q should be in the form of (state, action) pairs, where state is a tuple of all piles sizes in order, and action is a tuple (i, j) representing a pile and a number.

•	If no Q-value for the state/action pair exists in self.q, then the function should return 0.

The **update_q_value** function takes a state state, an action action, an existing Q value old_q, a current reward reward, and an estimate of future rewards future_rewards, and updates the Q-value for the state/action pair according to the Q-learning formula.

•	Recall that the Q-learning formula is: Q(s, a) <- old value estimate + alpha * (new value estimate - old value estimate)

•	Recall that alpha is the learning rate associated with the NimAI object.

•	The old value estimate is just the existing Q-value for the state/action pair. The new value estimate should be the sum of the current reward and the estimated future reward.

The **best_future_reward** function accepts a state as input and returns the best possible reward for any available action in that state, according to the data in self.q.

•	For any action that doesn’t already exist in self.q for the given state, you should assume it has a Q-value of 0.

•	If no actions are available in the state, you should return 0.

The **choose_action** function should accept a state as input (and optionally an epsilon flag for whether to use the epsilon-greedy algorithm), and return an available action in that state.

•	If epsilon is False, your function should behave greedily and return the best possible action available in that state (i.e., the action that has the highest Q-value, using 0 if no Q-value is known).

•	If epsilon is True, your function should behave according to the epsilon-greedy algorithm, choosing a random available action with probability self.epsilon and otherwise choosing the best action available.

•	If multiple actions have the same Q-value, any of those options is an acceptable return value.

A video Demonstrating the Functionality of this Project and be found at: https://youtu.be/1ZdkuFK7LZw