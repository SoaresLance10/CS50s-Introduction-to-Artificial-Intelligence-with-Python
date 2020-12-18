# Knights and Minesweeper
## Knights
In 1978, logician Raymond Smullyan published “What is the name of this book?”, a book of logical puzzles. Among the puzzles in the book were a class of puzzles that Smullyan called “Knights and Knaves” puzzles.

In a Knights and Knaves puzzle, the following information is given: Each character is either a knight or a knave. A knight will always tell the truth: if knight states a sentence, then that sentence is true. Conversely, a knave will always lie: if a knave states a sentence, then that sentence is false.

The objective of the puzzle is, given a set of sentences spoken by each of the characters, determine, for each character, whether that character is a knight or a knave.

For example, consider a simple puzzle with just a single character named A. A says “I am both a knight and a knave.”

Logically, we might reason that if A were a knight, then that sentence would have to be true. But we know that the sentence cannot possibly be true, because A cannot be both a knight and a knave – we know that each character is either a knight or a knave, but not both. So, we could conclude, A must be a knave.

That puzzle was on the simpler side. With more characters and more sentences, the puzzles can get trickier! Your task in this problem is to determine how to represent these puzzles using propositional logic, such that an AI running a model-checking algorithm could solve these puzzles for us.

The **specifications** for the project as mentioned at: https://cs50.harvard.edu/ai/2020/projects/1/knights/
### Specification
Add knowledge to knowledge bases **knowledge0**, **knowledge1**, **knowledge2**, and **knowledge3** to solve the following puzzles.

•	Puzzle 0 is the puzzle from the Background. It contains a single character, A.
1. A says “I am both a knight and a knave.”
•	Puzzle 1 has two characters: A and B.
1. A says “We are both knaves.”
2. B says nothing.
•	Puzzle 2 has two characters: A and B.
1. A says “We are the same kind.”
2. B says “We are of different kinds.”
•	Puzzle 3 has three characters: A, B, and C.
1. A says either “I am a knight.” or “I am a knave.”, but you don’t know which.
2. B says “A said ‘I am a knave.’”
3. B then says “C is a knave.”
4. C says “A is a knight.”
In each of the above puzzles, each character is either a knight or a knave. Every sentence spoken by a knight is true, and every sentence spoken by a knave is false.


A video Demonstrating the Functionality of this Project and be found at: https://youtu.be/urVm0_EKEgQ

## Minesweeper
Write an AI to play Minesweeper.

Minesweeper is a puzzle game that consists of a grid of cells, where some of the cells contain hidden “mines.” Clicking on a cell that contains a mine detonates the mine, and causes the user to lose the game. Clicking on a “safe” cell (i.e., a cell that does not contain a mine) reveals a number that indicates how many neighboring cells – where a neighbor is a cell that is one square to the left, right, up, down, or diagonal from the given cell – contain a mine.

The **specifications** for the project as mentioned at: https://cs50.harvard.edu/ai/2020/projects/1/minesweeper/
### Specification
Complete the implementations of the Sentence class and the MinesweeperAI class in minesweeper.py.

In the Sentence class, complete the implementations of **known_mines**, **known_safes**, **mark_mine**, and **mark_safe**.

•	The known_mines function should return a set of all of the cells in self.cells that are known to be mines.
•	The known_safes function should return a set of all the cells in self.cells that are known to be safe.
•	The mark_mine function should first check to see if cell is one of the cells included in the sentence.
1. If cell is in the sentence, the function should update the sentence so that cell is no longer in the sentence, but still represents a logically correct sentence given that cell is known to be a mine.
2. If cell is not in the sentence, then no action is necessary.
•	The mark_safe function should first check to see if cell is one of the cells included in the sentence.
1. If cell is in the sentence, the function should update the sentence so that cell is no longer in the sentence, but still represents a logically correct sentence given that cell is known to be safe.
2. If cell is not in the sentence, then no action is necessary.


In the MinesweeperAI class, complete the implementations of **add_knowledge**, **make_safe_move**, and **make_random_move**.

•	add_knowledge should accept a cell (represented as a tuple (i, j)) and its corresponding count, and update self.mines, self.safes, self.moves_made, and self.knowledge with any new information that the AI can infer, given that cell is known to be a safe cell with count mines neighboring it.
1. The function should mark the cell as one of the moves made in the game.
2. The function should mark the cell as a safe cell, updating any sentences that contain the cell as well.
3. The function should add a new sentence to the AI’s knowledge base, based on the value of cell and count, to indicate that count of the cell’s neighbors are mines. Be sure to only include cells whose state is still undetermined in the sentence.
4. If, based on any of the sentences in self.knowledge, new cells can be marked as safe or as mines, then the function should do so.
5. If, based on any of the sentences in self.knowledge, new sentences can be inferred (using the subset method described in the Background), then those sentences should be added to the knowledge base as well.
6. Note that any time that you make any change to your AI’s knowledge, it may be possible to draw new inferences that weren’t possible before. Be sure that those new inferences are added to the knowledge base if it is possible to do so.
•	make_safe_move should return a move (i, j) that is known to be safe.
1. The move returned must be known to be safe, and not a move already made.
2. If no safe move can be guaranteed, the function should return None.
3. The function should not modify self.moves_made, self.mines, self.safes, or self.knowledge.
•	make_random_move should return a random move (i, j).
1. This function will be called if a safe move is not possible: if the AI doesn’t know where to move, it will choose to move randomly instead.
2. The move must not be a move that has already been made.
3. The move must not be a move that is known to be a mine.
4. If no such moves are possible, the function should return None.


A video Demonstrating the Functionality of this Project and be found at: https://youtu.be/eN9WUScIMtY
