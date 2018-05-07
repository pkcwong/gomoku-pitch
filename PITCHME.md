# Gomoku AI

An overly simplified approach.

<div style="float: right">
  Christopher Wong
</div>

---

## The Game

Gomoku is a game where players fight to put 5 stones in a row.

- horizontal
- vertical
- diagonal

---

## Visualization

- Permutate all winning combinations
- Window of "5"s

---


A | B | C | D | E
--- | --- | --- | --- | ---
X | X | . | X | X

This is an 80% complete, possible winning "window".


A | B | C | D | E
--- | --- | --- | --- | ---
X | O | . | X | X

This is a 60% complete, impossible winning "window".

---

## The Heuristic

For each possible winning "window", a score is given based on the completeness.

completeness | score (gote~sente)
--- | ---
0% | 0 ~ 0
20% | 1 ~ 2
40% | 100 ~ 2000
60% | 4000 ~ ```INT_MAX``` / 32
80% | ```INT_MAX``` / 16 ~ ```INT_MAX``` / 8

---

## Implementation

The trivial way of defining a board would be using ```char[][]```, updating the cells as the game progress.

```C
  Engine::Engine(int size) : BOARD_SIZE(size) {
  	this->board = new char* [size];
  	for (int i = 0; i != size; i++) {
  		this->board[i] = new char[size];
  		for (int j = 0; j != size; j++) {
  			this->board[i][j] = ' ';
  		}
  	}
  }
```

---

## Computing the Heuristic Score

- Each stone only "affects" a 5 by 5 area.
- More precisely, only a range of 5 in 8 directions.
- A 2D array is used to store scores at different cells.

---

Define ```score[][]``` as follows.

```C
  score[i][j] =
    heuristic(board[i][j] ~ East) +
    heuristic(board[i][j] ~ SouthEast) +
    heuristic(board[i][j] ~ South) +
    heuristic(board[i][j] ~ SouthWest)
```

For each move, only 17 cell updates are necessary, as opposed to updating the score of the entire board.
