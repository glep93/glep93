---
title:  "How to beat Beth Harmon"
subtitle: "Develop a chess engine and let it play on chess.com"
image: "images/chess.jpg"
date:   2020-01-03 00:00:00
layout: post
---

After the success of *The queen's gambit* the chess game acquired a new success. The web
site *chess.com* offers the possibility to play with bots that play like Beth Harmon
at different ages. To face this challenge I developed a small chess engine able to
play with *chess.com* bots.  

### The chess engine

In the last years, a lot of presentations about Artificial Intelligence starts with
a slide with a Venn diagram like the following:

<img src="https://glep93.github.io/glep93//images/ai-ml-dl.png" width="100%">

I don't usually like this Venn diagram, it suggests the existence of AI models that
are not ML models and it opens up huge futile discussions about what it is and what it isn't ML...
Approaching this project I found that the *classic* chess engines are a beautiful
example of Artificial Intelligence models that are not ML. Indeed, classic chess engines
are not trained on data and so they are **not machine learning models**.
However, after the appearance of *Leela Chess Zero* in 2018 it appears a new generation of
chess engines based on deep learning techniques that learn to play chess looking at a huge
quantity of games.

For this project, I focused on classic chess engines similar to Deep Blue, the
chess computer that beat the world champion, Garry Kasparov, in 1996.

#### Game tree

A game tree is the representation of all possible matches in a game such as tic-tac-toe,
connect four, chess, or go. Any node in the tree represents a possible configuration of the board
(and history to arrive at this configuration), the edges represent the
legal moves leading from one configuration to the next.

<figure>
<img src="https://glep93.github.io/glep93/images/chess_Game_tree.svg" width="100%">
 <figcaption>First 2 move in chess game.</figcaption>
 </figure>


In principle, if you can write the entire game tree of a game you have just resolved the chess game,
you can look at the tree to find the best move in any situation. The only problem
is that the game tree for chess is huge, it is estimated that it is more than 10<sup>120</sup> (https://en.wikipedia.org/wiki/Shannon_number) considering that the estimation of atoms in the universe is  10<sup>80</sup>! So clearly it is not possible to write down the entire chess game
tree. A solution is to compute the game tree only for a certain number of possible
moves from the current position (in 1997 deep blue search to a depth of between 12 and 16 moves).

The leaves of a game-tree are end-game configurations with the win of one of the two players or a draw.
If you compute the game tree only at a certain depth you need an **evaluation function**
to estimate how good is a leaf of the pruned tree.

#### Evaluation function

The evaluation function \\( f \\) is function from chess board configuration set \\( B \\) to real numbers \\( R \\).
Usually it is write in a whay that \\( f(x) > f(y) \\) if \\( x \\) is a better
connfiguration then \\( y \\)  for white, morehover  \\( f(x) \rightarrow \infty \\)
if \\(x \\) is a winning configuration for white and \\(f(x) \rightarrow -\infty  \\) if it is a winning
configuration for black.
