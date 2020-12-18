# Degrees and Tic-Tac-Toe
## Degrees
According to the Six Degrees of Kevin Bacon game, anyone in the Hollywood film industry can be connected to Kevin Bacon within six steps, where each step consists of finding a film that two actors both starred in.

In this problem, we’re interested in finding the shortest path between any two actors by choosing a sequence of movies that connects them. For example, the shortest path between Jennifer Lawrence and Tom Hanks is 2: Jennifer Lawrence is connected to Kevin Bacon by both starring in “X-Men: First Class,” and Kevin Bacon is connected to Tom Hanks by both starring in “Apollo 13.”

We can frame this as a search problem: our states are people. Our actions are movies, which take us from one actor to another (it’s true that a movie could take us to multiple different actors, but that’s okay for this problem). Our initial state and goal state are defined by the two people we’re trying to connect. By using breadth-first search, we can find the shortest path from one actor to another.


The **specifications** for the project as mentioned at: https://cs50.harvard.edu/ai/2020/projects/0/degrees/
### Specification
Complete the implementation of the **shortest_path** function such that it returns the shortest path from the person with id source to the person with the id target.

•	Assuming there is a path from the source to the target, your function should return a list, where each list item is the next (movie_id, person_id) pair in the path from the source to the target. Each pair should be a tuple of two ints.

•	For example, if the return value of shortest_path were [(1, 2), (3, 4)], that would mean that the source starred in movie 1 with person 2, person 2 starred in movie 3 with person 4, and person 4 is the target.

•	If there are multiple paths of minimum length from the source to the target, your function can return any of them.

•	If there is no possible path between two actors, your function should return None.

•	You may call the neighbors_for_person function, which accepts a person’s id as input, and returns a set of (movie_id, person_id) pairs for all people who starred in a movie with a given person.

A video Demonstrating the Functionality of this Project and be found at: https://youtu.be/xXFBrTKqecY

## Tic-Tac-Toe
Using Minimax, implement an AI to play Tic-Tac-Toe optimally.

The **specifications** for the project as mentioned at: https://cs50.harvard.edu/ai/2020/projects/0/tictactoe/
### Specification
Complete the implementations of **player**, **actions**, **result**, **winner**, **terminal**, **utility**, and **minimax**.

•	The player function should take a board state as input, and return which player’s turn it is (either X or O).
1. In the initial game state, X gets the first move. Subsequently, the player alternates with each additional move.
2. Any return value is acceptable if a terminal board is provided as input (i.e., the game is already over).
The actions function should return a set of all of the possible actions that can be taken on a given board.

•	Each action should be represented as a tuple (i, j) where i corresponds to the row of the move (0, 1, or 2) and j corresponds to which cell in the row corresponds to the move (also 0, 1, or 2).
1. Possible moves are any cells on the board that do not already have an X or an O in them.
2. Any return value is acceptable if a terminal board is provided as input.

•	The result function takes a board and an action as input, and should return a new board state, without modifying the original board.
1. If action is not a valid action for the board, your program should raise an exception.
2. The returned board state should be the board that would result from taking the original input board, and letting the player whose turn it is make their move at the cell indicated by the input action.
3. Importantly, the original board should be left unmodified: since Minimax will ultimately require considering many different board states during its computation. This means that simply updating a cell in board itself is not a correct implementation of the result function. You’ll likely want to make a deep copy of the board first before making any changes.

•	The winner function should accept a board as input, and return the winner of the board if there is one.
1. If the X player has won the game, your function should return X. If the O player has won the game, your function should return O.
2. One can win the game with three of their moves in a row horizontally, vertically, or diagonally.
3. You may assume that there will be at most one winner (that is, no board will ever have both players with three-in-a-row, since that would be an invalid board state).
4. If there is no winner of the game (either because the game is in progress, or because it ended in a tie), the function should return None.

•	The terminal function should accept a board as input, and return a boolean value indicating whether the game is over.
1. If the game is over, either because someone has won the game or because all cells have been filled without anyone winning, the function should return True.
2. Otherwise, the function should return False if the game is still in progress.

•	The utility function should accept a terminal board as input and output the utility of the board.
1. If X has won the game, the utility is 1. If O has won the game, the utility is -1. If the game has ended in a tie, the utility is 0.
2. You may assume utility will only be called on a board if terminal(board) is True.

•	The minimax function should take a board as input, and return the optimal move for the player to move on that board.
1. The move returned should be the optimal action (i, j) that is one of the allowable actions on the board. If multiple moves are equally optimal, any of those moves is acceptable.
2. If the board is a terminal board, the minimax function should return None.

A video Demonstrating the Functionality of this Project and be found at: https://youtu.be/3lxyx9E84a0
