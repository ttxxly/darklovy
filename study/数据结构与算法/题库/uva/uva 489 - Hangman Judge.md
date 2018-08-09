In “Hangman Judge,” you are to write a program that judges a series of Hangman games. 

在“刽子手”游戏中，你要写一个程序来判断一系列的刽子手游戏。

For each game, the answer to the puzzle（难题） is given as well as the guesses. Rules are the same as the classic game of hangman, and are given as follows:

对于每一款游戏，游戏的答案和猜测都是一样的。游戏规则与经典的刽子手游戏规则相同，如下所列:

1. The contestant tries to solve to puzzle by guessing one letter at a time.
2. Every time a guess is correct, all the characters in the word that match the guess will be “turned
  over.” For example, if your guess is ‘o’ and the word is “book”, then both ‘o’s in the solution will
  be counted as “solved”.
3. Every time a wrong guess is made, a stroke will be added to the drawing of a hangman, which
  needs 7 strokes to complete. Each unique wrong guess only counts against the contestant once.


4. If the drawing of the hangman is completed before the contestant has successfully guessed all the
  characters of the word, the contestant loses.

5. If the contestant has guessed all the characters of the word before the drawing is complete, the
  contestant wins the game.

6. If the contestant does not guess enough letters to either win or lose, the contestant chickens out.
  Your task as the “Hangman Judge” is to determine, for each game, whether the contestant wins,
  loses, or fails to finish a game.
  Input
  Your program will be given a series of inputs regarding the status of a game. All input will be in lower
  case. The first line of each section will contain a number to indicate which round of the game is being
  played; the next line will be the solution to the puzzle; the last line is a sequence of the guesses made
  by the contestant. A round number of ‘-1’ would indicate the end of all games (and input).
  Output
  The output of your program is to indicate which round of the game the contestant is currently playing
  as well as the result of the game. There are three possible results:
  You win.
  You lose.
  You chickened out.

  ![20180204213337](F:\Alan li\图片\20180204213337.jpg)

  ​

#### 大致题意

刽子手游戏其实是一款猜单词游戏，如图所示。游戏规则是：计算机想一个单词让你猜，你每次可以猜一个字母，如果单词里有那个字母，那么单词中所有该字母都会显示出来；如果没有那个字母，则计算机会在一幅“刽子手”画上添一笔。这幅画一共需要7笔才能完成，因此你最多可以错6次。注意，猜一个已经猜过的字母也算错。

在本题中，你的任务是编写一个裁判程序，输入单词和玩家的猜测，判断玩家赢了(You win,)、输了(You lose.)还是放弃了(You chicked out.)。每组数字包含3行。第一行是游戏编号(-1为输入结束标记),第二行是计算机想的单词，第三行是玩家的猜测。后两行保证只含小写字母。

#### Sample Input

```
1
cheese
chese
2
cheese
abcdefg
3
cheese
abcdefgij
-1
```

#### Sample Output

```
Round 1
You win.
Round 2
You chickened out.
Round 3
You lose.
```

