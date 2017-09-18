Word Search Kata
================
In this exercise you will build a program to complete a [word search](https://en.wikipedia.org/wiki/Word_search) problem.

Given a text file consisting of a list of words, and a series of rows of single-character lists representing the word search grid, this program should search for the words in the grid and return a set of x,y coordinates for each word found.

The point of this kata to to provide a larger than trivial exercise that can be used to practice TDD. A significant portion of the effort will be in determining what tests should be written and, more importantly, written next.

## Input ##

The first line of the text file will consist of the list of words to be found.  The following lines will consist of a list of single characters, A-Z. All lines in the file except the first will have the same length, and the number of rows will match the number of characters in a line.  This input represents the square grid of the word search.

The grid will always be square, and all words in the list will always be present in the grid. Words may be located horizontally, vertically, diagonally, and both forwards and backwards.  Words will never "wrap" around the edges of the grid.

The following is an example of the format of the input file:

<pre>
BONES,KHAN,KIRK,SCOTTY,SPOCK,SULU,UHURA
U,M,K,H,U,L,K,I,N,V,J,O,C,W,E
L,L,S,H,K,Z,Z,W,Z,C,G,J,U,Y,G
H,S,U,P,J,P,R,J,D,H,S,B,X,T,G
B,R,J,S,O,E,Q,E,T,I,K,K,G,L,E
A,Y,O,A,G,C,I,R,D,Q,H,R,T,C,D
S,C,O,T,T,Y,K,Z,R,E,P,P,X,P,F
B,L,Q,S,L,N,E,E,E,V,U,L,F,M,Z
O,K,R,I,K,A,M,M,R,M,F,B,A,P,P
N,U,I,I,Y,H,Q,M,E,M,Q,R,Y,F,S
E,Y,Z,Y,G,K,Q,J,P,C,Q,W,Y,A,K
S,J,F,Z,M,Q,I,B,D,B,E,M,K,W,D
T,G,L,B,H,C,B,E,C,H,T,O,Y,I,K
O,J,Y,E,U,L,N,C,C,L,Y,B,Z,U,H
W,Z,M,I,S,U,K,U,R,B,I,D,U,X,S
K,Y,L,B,Q,Q,P,M,D,F,C,K,E,A,B
</pre>

## Output ##
The output of the program is the location of each word found, each on a separate line.  The location will be represented as a series of x,y coordinates, where both x and y start at zero at the top-left of the grid.  From this position both x and y will increase, i.e. they will never be negative.  

Given the example input above, the following output would be expected:

<pre>
BONES: (0,6),(0,7),(0,8),(0,9),(0,10)
KHAN: (5,9),(5,8),(5,7),(5,6)
KIRK: (4,7),(3,7),(2,7),(1,7)
SCOTTY: (0,5),(1,5),(2,5),(3,5),(4,5),(5,5)
SPOCK: (2,1),(3,2),(4,3),(5,4),(6,5)
SULU: (3,3),(2,2),(1,1),(0,0)
UHURA: (4,0),(3,1),(2,2),(1,3),(0,4)
</pre>

## User Stories ##
*As the Puzzle Solver*<br />
*I want to search horizontally*<br />
*So that I can find words on the X axis*<br />

*As the Puzzle Solver*<br />
*I want to search vertically*<br />
*So that I can find words on the Y axis*<br />

*As the Puzzle Solver*<br />
*I want to search diagonally descending*<br />
*So that I can find words the descend along the X axis*<br />

*As the Puzzle Solver*<br />
*I want to search diagonally ascending*<br />
*So that I can find words that ascend along the X axis*<br />

*As the Puzzle Solver*<br />
*I want to search backwards*<br />
*So that I can find words in reverse along all axes*<br />

## FAQ ##

*It looks hard to generate test data.  How can do do this easily?*<br />
* If you need to generate test data there are many sites which will generate puzzles for you, such as [this one](http://puzzlemaker.discoveryeducation.com/WordSearchSetupForm.asp?campaign=flyout_teachers_puzzle_wordcross).

*How large can the grid be?*<br />
* Big or small, this is really up to you as long as you remember that the grid will always be square and that your solution should meet the requirements described above. This question is really outside the scope of the kata; the point is to focus on Test-Driving and software craftsmanship.

*How long or short can the words be?*<br />
* Words will be a minimum of two letters long, and will always fit within the grid along the axis on which it can be located.

James Prior's kata
==================

The following is how I did this kata in Python3 from scratch.

Normally, one would not include versions of code that make tests fail,
but failing versions of code are included in this repository
so that one can see the process.

The order of the TDD stuff was roughly:
- (start-here) Install stuff.
- (step-1) create many separate tests.
  The code that the tests are for does not exist yet.
  So the tests fail.
- (step-2) Created a stub function to make tests fail.
- (step-3) Put meat in the function to make all the tests pass.
That's the basics, which one repeats over and over.
One can also refactor the code, repeating step-3 over and over.

Then I added some more tests and
- (step-4) Add more tests for bad input values.
- (step-5) Change the code to make the tests pass.

## Installation

The following instructions work on Knoppix 7.7.1 live DVD.
One can boot actual media such as a DVD or a USB flash drive on an actual PC,
or boot the ISO-9660 image of the DVD in a virtual machine.
The latter is probably more practical for most people
as it allows those with various operating systems,
such as macOS, Microsoft Windows, and Linux,
to play without disturbing their host operating systems.

```
git clone https://github.com/james-prior/kata-word-search.git
source kata-word-search/setup
```

## Dependencies

```
- virtualenv
- git
- Python 3 with the following packages
  - apipkg==1.4
  - execnet==1.4.1
  - py==1.4.34
  - pytest==3.2.2
  - pytest-forked==0.2
  - pytest-xdist==1.20.0
- optional
  - meld
```

## Setup

```
# Use three terminal emulators.

# in terminal emulator 1:
cd kata-word-search
git checkout start-here

# in terminal emulator 2:
# This pane shows results of tests that are run each time a file is changed.
cd kata-word-search
source env/bin/activate
py.test -f .

# in terminal emulator 3:
cd kata-word-search
watch 'git status'

# in terminal emulator 1:
# Now do a mix of vi, git add, git commit, and git status commands.

# The following commands are handy for seeing the differences between versions.
git diff dev^ dev
git difftool -t meld -y dev^ dev
# Unfortunately, meld is not available on Knoppix
```
