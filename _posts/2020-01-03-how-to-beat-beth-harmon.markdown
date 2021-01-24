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
example of Artificial Intelligence models that are not ML, and almost every one agree about it
reducing futile discussiona. Indeed, classic chess engines
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
  <br>

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
Usually it is write in a way that \\( f(x) > f(y) \\) if \\( x \\) is a better
connfiguration then \\( y \\)  for white, morehover  \\( f(x) \rightarrow \infty \\)
if \\(x \\) is a winning configuration for white and \\(f(x) \rightarrow -\infty  \\) if it is a winning
configuration for black.
The moste simple evaluation function can be read as:

$$f(board) = \begin{cases} \infty, & \mbox{if } \mbox{ white wins}
 						 \\ -\infty , & \mbox{if } \mbox{ balck wins}
 						 \\ 0, & \mbox{if } n\mbox{ draw}
 						 \\ N_{white}- N_{black},  n\mbox{ else} 
 						  \end{cases} $$

Where  \\(N_{white/black}  \\) are the number of pieces for each player. I actualy use a slightly most
difficult evaluate function inspired from [here.](https://www.chessprogramming.org/Simplified_Evaluation_Function)


### Search algorithm

 Now that we have an effective representation of the game and an evaluation function,
  all that's left is to apply an algorithm that finds the right move to make. 
 
 I have applied several algorithms for this purpose minmax, alphabet pruning,
  MTD-inf and MTD-bi, but for the purpose of this article I will just tell you 
  about minmax. 
 
 The minmax algorithm is a greedy algorithm that approaches the problem without
 any finesse. The only idea on which it is based is that the white player will 
 make his moves in order to maximize the evaluation function, while the black player 
 to minimize.

 The first step is to "unfold" the wire tree to the maximum depth we want to reach 
 (in example 4), evaluate the leaves with our evaluation function and then reconstruct 
 the best path from the bottom, remembering that the black player (represented by the 
 diamonds in the graph below) minimizes, while the white player (represented by the 
 ellipse-shaped nodes) maximizes.

 <figure>
 <img src="/images/minmax_movie.gif" width="100%">
  <figcaption>min max algorithm example</figcaption>
  </figure>


### Let's see it in action agains Beth Harmon

So, with the help of selenium I made my chess engine interface with the site so that
automatically the two bots can clash. 

 <figure>
<iframe width="420" height="315"  src="http://www.youtube.com/embed/0v4bmEGi--U"  
width="100%" 
margin-left="auto"
margin-right="auto"
 frameborder="0" allowfullscreen></iframe>
 </figure>
  <br>

If you would try to beat yourserlf Beth Harmon with python please check 
[my repository.](https://github.com/glep93/python_chess_engine)