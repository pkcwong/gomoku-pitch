# Gomoku AI

An overly simplified approach.

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
--- | ---| --- | --- | ---
X | X |   | X | X

This is an 80% complete, possible winning "window".


A | B | C | D | E
--- | ---| --- | --- | ---
X | O |   | X | X

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
