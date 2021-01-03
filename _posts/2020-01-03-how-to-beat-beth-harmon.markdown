---
title:  "How to beat Beth Harmon"
subtitle: "Develop a chess engine and let it play on chess.com"
image: "images/chess.jpg"
date:   2020-01-03 00:00:00
---

After the success of *The queen's gambit* the chess game acquired a new success. The web
site *chess.com* offer the possibility to play with bots that plays like Beth Harmon
at different ages. To face this challenge I developed a small chess engine able to
play with *chess.com* bots.  

### The chess engine

In the last years a lot of presentations about Artificial Intelligence starts with
a slide with a Venn diagram like the following:

![AI, ML and DL](/images/ai-ml-dl.png)

I don't usually like this Venn diagram, it suggests the existence of AI models that
are not ML models and it opens up huge futile discussions about what it is and what it isn't.
Approaching this project I actually found that the *classic* chess engines are a beautefull
example of Artificial Intelligence models that are not ML. Indeed, classic chess engines
are not trained looking on data and so they are clearly **not a machine learning models**.
However after the appear of *Leela Chess Zero* in 2018 it appears a new generation of
chess engine based on deep learning tecniques that learn to play chess looking a huge
quantity of games.

For this project I focused on classic chess engines similar to Deap Blue, the
chess computer that beat world champion Garry Kasparov in 1996.

#### Game tree

A game tree is the representation of all possible matches in a game such as tic-tac-toe,
conect four, chess or go. Any node in the tree represents a possible configuration of the board
(and history to arrive at this configuration), the edges represent the
legal moves leading from one configuration to the next.

![chess tree](/images/chess_Game_tree.svg)

In principle if you can write the entire game tree of a game you have resolve it,
you can look at the tree to find the best move in any situation. The only problem
is that the game tree for chess is huge, it is extiamte that it is more then 10<sup>120</sup> (https://en.wikipedia.org/wiki/Shannon_number) considering that extimation of atoms in the universe is  10<sup>80</sup>! So clearly it is not possible to write down the entire chess game
tree. A solution is to write compute the game tree only for a certain number of possible
moves from the current position (in 1997 deep blue search to a depth of between 12 and 16 moves).

The leaf of the a game-tree are end-game configurations with the win of one of the two players or a draw.
If you compute the game tree only at a certain depth you need an **evaluation function**
to extimate how good is a leaf of the pruned tree.

#### Evaluation function

The evaluation function \\[ a^2 = b^2 + c^2 \\] is function from chess board configuration set to real numbers.
Usually it is write in a whay that
