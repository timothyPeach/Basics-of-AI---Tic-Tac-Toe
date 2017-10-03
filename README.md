# ticTacToe-simple-optimal

So this is an optional project I was assigned at General Assembly's Data Science Immersive, and it's less about Data Science, but
I really like it because the solution I found is pretty elegant.

The goals were:

1) Make an interface where you can play Tic Tac Toe in Python.
2) Make a computer that plays against you.
3) Make the computer AI play /perfectly/.

The first two were pretty basic to do, but the third part is pretty interesting.

My first thought was to look online and read some articles about how to play tic tac toe well, and see if someone had
distilled it down to a few very simple rules, but honestly all the articles I read were terrible.

After reading this, you will /actually/ understand tic tac toe, and it will never be confusing where to move, because
rather than memorizing some dumb order of moves, there's just a general rule that SUMS up the whole game! (literally lol)

After thinking about it for a bit, I realized you can break the board down into 8 "Winning Lanes."  There are 3 Horizontal Lanes,
3 Vertical Lanes, and 2 Diagonal Lanes.

And so the first thing to realize about the game is... say you're playing as X... you can't lose in one of these Lanes if you
have an X in it! After all, your opponent needs to have three O's in a row, right?

This being the case, the optimal strategy is to take up as many lanes as possible all the time.  That's why it's best to
go in the center for your first move.  You're in 4 lanes.  The 2 Vertical and Horizontal Lanes that involve the middle spot.

And that's also why it's best as Player 2, after Player 1 takes the center, to take one of the corner spots, because you're
occupying 3 lanes if you take the corner, but only 2 lanes if you go somewhere else.

And so all I did was create a scoring system for each lane:

Let's imagine the Top Horizontal Lane.  At the beginning of the game, it looks like this:  _ _ _  and has a score of 0.

Nobody has gone anywhere yet.

Say we go in the leftmost spot:  X _ _

Well, I'm gonna give that some score like 1.

And we will evaluate this move across all lanes.  This X is also in the leftmost Vertical Lane, and it's in one of the 2
Diagonal Lanes, and so those 3 lanes all have a score of 1.

If we add up all the lanes now, we have a score of 3.

The bot will try all moves and find that moving in the Center is the best, with a score of 4.

Here are some of the other scorings:

X O _ (scored as 0 because no one can win in this lane)

X O O (also scored as 0 for same reason)

X X _ (scored as 10 because we're 1 away from winning!)

O O _ (scored as -10 because we're 1 move away from losing!)

X X X (scored as 1000 or something like this because we win.)

O O O (-1000, same idea, we want to avoid this at all costs.)

An interesting thing that the bot does.

Consider the following board state where it is X to move:

_ O _

X X O

_ _ _.

O hasn't played too well... On O's first move, he didn't go in the corner, and now X can either go in the upper left square,
or the lower left square, and create a situation where TWO WINS are possible!

Let's look at both of those so it's more clear:

_ O _

X X O

X _ _

What is O supposed to do here?  If O blocks the upper left spot, X just wins by going in the upper right spot! The game is over!

Here's the other way X can win:

X O _

X X O

_ _ _.

An identically terrible situation for O, but with one important difference!

The bot will always choose to move here, because not only does it create two ways of winning the game, but it blocks O's
only unoccupied lane because it is worth 1 more point.  Not only does the bot play perfectly, it takes away everything
from the opponent that it can even when it is unnecessary. Like y u so mean let him have a lane omg lol.

Well that's about it! Hope you enjoyed!
