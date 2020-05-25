---
layout: single
title: "Python for Beginners: Candyland"
date: 2020-05-10 19:55:00 -0700
categories: games beginner-python
permalink: /candyland
---
When I was young, Candy Land was one of my favorite board games to play with my family. I was always so excited when I drew one of the fancy character cards or a double color card. I think I also liked it because there aren't really too many opportunities to cheat (Not that it's impossible, just more difficult) which is advantageous when playing with competitive siblings. Today I'm going to try and implement a basic version of Candy Land in Python. Hopefully we have fun and learn some new Python tricks along the way.

![Candyland](https://images-na.ssl-images-amazon.com/images/I/91yUG40gv0L._AC_SX425_.jpg)

Developed by:
    - Austin Montgomery
Date: 13 May 2020

## Introduction

In my last [beginner Python post](https://bigmonty12.github.io/battleship), we made a basic Python version of Battleship. We focused on functions, lists, and if-else statements. We'll continue to see those aspects, but we're also going to learn a little about dictionaries, classes, and numpy arrays.

### Dictionaries

We saw before how lists can be used as a way to store information.
```
nba_teams = ['Spurs', 'Jazz', 'Knicks']
```
Dictionaries are similar to lists in that they store objects; however, they can store information in a different way. Dictionaries let us map objects to other objects. Traditionally, we call these keys and values. We have one object, a key, and anything that is associated with it, its value. Let's build on our NBA example.
```
nba_rankings = {'Spurs': 'Best', 'Jazz': 'Average', 'Knicks': 'Worst'}
```
One difference we note right away is that instead of square brackets [ ], we have curly brackets { }. We also see colons. We turned our list of NBA teams into keys (the team name) and then gave each team a value (their ranking). This is pretty useful! Let's say we wanted to know how good the San Antonio Spurs are. All we have to type is:
```
nba_rankings['Spurs']
```
And our result is:

'Best'

![spurs](https://cdn.vox-cdn.com/thumbor/wOUSMeU-dQ3MKwk9EwZzNe6o-A8=/0x0:980x979/1200x800/filters:focal(400x190:556x346)/cdn.vox-cdn.com/uploads/chorus_image/image/65941744/tim_duncan_5_championships.0.jpg)

We can also see the different keys, values, and items (tuples of keys with associated values) with these methods
```
nba_rankings.keys()
nba_rankings.values()
nba_rankings.items()
```

Those are the basics of dictionaries! We use them quite often so there will be ample opportunity to practice!

### Classes

Classes are a way to bundle data and functionality. They can be tough to get a handle on at first so I'll demonstrate first.
```
class Team():

    def __init__(self, name):
        self.name = name
    
    def printName(self):
        print(self.name)

best_team = Team('Spurs')
best_team.printName()
```
I like to use classes when I will be using similar objects that differ slightly. With a class, you can set up all the background details you want all the objects of this type of class (say NBA teams) to have. With the NBA team example, I would want to make sure each team object has information about coaches, players, location, etc. Let's look at the structure of the class above. First we can name the general class with `class Team():`. This is pretty straightforward; we're just telling our code that the object we're about to build is a class. Now the first function we pretty much always see when building a class is `def __init_(self, etc):`. This is our *init*ialization method, or how we build the 'under the hood' part of our class. Notice the first parameter is `self`. Common practice says to use `self`, but technically you can use any word: You just have to stay consistent for the rest of the class. `self` is essentially the parameter which tells the class that these functions should be called on itself. `self` is also used with descriptors like we saw with `self.name`. That means our class objects have a name attribute available to us. In our above example, we can say:
```
best_team.name
```
And we will get 'Spurs'.
![team](https://miro.medium.com/max/450/1*hW9gzi2dCHdKUWy4vsIs0A.jpeg)

Our last thing to address from our example is `def printName(self)`. When we create functions in a class, these are known as methods. We've seen methods before with lists (and dictionaries) such as `list.append()`. It can be pretty useful to have these built-in methods as we'll see later in our game.

### NumPy Arrays

NumPy is a fundamental scientific computing package in Python. It's especially known for large, multi-dimensional arrays and matrices. NumPy arrays are rather similar to lists except they work much faster with less memory and are more convenient to use, particularly when math is involved. That's all we really need to know about NumPy arrays right now, but there's a good chance we'll run into them again one day.

## Candy Land
Now that we've learned about dictionaries and classes, let's get to work on Candy Land!

### Objective
Build a game with different kinds of cards (single colors, double colors, and special characters) that multiple characters can use to advance to the end of the game.

Let's first bring in the extra packages we'll need. The `random` package will help us make our game fair and lead to randomly drawn cards. We `import numpy as np` so we don't have to type out numpy anytime we want to use something from the package. 


```python
import random
import numpy as np
```

Let's first create a board. The foundation of a Candy Land board is created by the colors of the spaces as well as the special characters. I've included the colors and characters below, but you can use any colors or characters you want! I've put my characters into a dictionary so I can store their respective space number on the board. I used `random.randint` to choose to their spaces. I've chosen to have each colored space repeat 25 times (`board = colors * 25`) but feel free to make it as long or short as you want! Finally, we want to put our special characters in their correct spot on the board.
```
for key, value in candyPeople.items():
    board[value] = key
```
Remember, `candyPeople.items()` will return a tuple of each key with its associated value. We can then use the value (the randomly assigned number) to index into our list and change the current value to our character's name! Using our characters and their spaces, this would look like:
```
board[21] = 'Plumpy'
board[33] = 'Mr. Mint'
board[57] = 'Gramma Nutt'
```
and so on.


```python
def createBoard():
    colors = ['Red', 'Purple', 'Yellow', 'Blue', 'Orange', 'Green']
    candyPeople = {'Plumpy': 21, 'Mr. Mint': 33, 'Jolly': 57, 'Gramma Nutt': 84, 'Princess Lolly': 93, 
               'Queen Frostine': 120}
    board = colors * 25
    board = np.array(board, dtype="<U14")
    for key, value in candyPeople.items():
        board[value] = key
    return board
```

Let's move on to building our Deck class! In our `__init__`, let's put in our colors, characters, a deck pile and a discard file, and two methods (`buildDeck` and `shuffleDeck`) we'll build. We want these methods in our `__init__` because we want our deck to be built and shuffled automatically when we make our class object. In `buildDeck`, we use for loops to add 6 single color cards and 4 double colors cards. We'll also add our character cards and give them the color 'Pink' so we can be consistent with every card having a color. Our `shuffleDeck` method is easy because the `random` package already has a shuffle function! Now if our deck is empty (which we check with `isEmpty`, we need to reshuffle our deck. In `reshuffleDeck`, we'll change our discard pile to our deck pile and then call our `shuffleDeck` method again. Finally, we should be able to draw cards with our characters. First, we check if our deck is empty. Then we use the `.pop` list method to give us the last card in our deck list. Then we move the card to the discard pile! 


```python
class Deck():
    
    def __init__(self):
        self.colors = ['Red', 'Purple', 'Yellow', 'Blue', 'Orange', 'Green']
        self.candyPeople = ['Plumpy', 'Mr. Mint', 'Jolly', 'Gramma Nutt', 'Princess Lolly', 'Queen Frostine']
        
        self.deck = []
        self.discard = []
        
        self.buildDeck()
        self.shuffleDeck()
        
    def buildDeck(self):
        for color in self.colors:
            for i in range(6):
                self.deck.append((color, 1))
            for i in range(4):
                self.deck.append((color, 2))
        for char in self.candyPeople:
            self.deck.append(('Pink', char))
        
    def shuffleDeck(self):
        random.shuffle(self.deck)
        random.shuffle(self.deck)
        random.shuffle(self.deck)
        
    def reshuffleDeck(self):
        self.deck = self.discard
        self.discard = []
        self.shuffleDeck()
        
    def isEmpty(self):
        return len(self.deck) == 0
    
    def drawCard(self):
        if self.isEmpty():
            self.reshuffleDeck()
        card = self.deck.pop()
        self.discard.append(card)
        return card 
```

Now let's create our Player class! We really only need to know a player's name and position so we'll put those in our `__init__` method. Let's put each player's position at -1 since the game hasn't started yet. The two other things players can do are print their card and move. The `printCard` method is fairly self-explanatory so let's go through the `move` method. If our card's color is 'Pink', then we know it's a special character card so let's move our player to that position on the board. If it's not 'Pink', then we see check where those next color spaces are on the board and then move either the 1 or 2 spaces our card says. If there are no more of those color spaces, then we move to the end of the board (meaning we've won!).


```python
class Player():
    def __init__(self, name):
        self.name = name
        self.pos = -1
        
    def printCard(self, card):
        if card[1] == 1:
            print(f'{self.name}: You drew a single {card[0]}! Advance to the next {card[0]}!')
        elif card[1] == 2:
            print(f'{self.name}: You drew a double {card[0]}! Advance two {card[0]}s!')
        else:
            print(f'{self.name}: You drew the {card[1]} card! Go to {card[1]}!')
            
        
    def move(self, card):
        if card[0] == 'Pink':
            self.pos = np.where(board == card[1])[0][0]
            print(f'Your new position is {self.pos}!')
            return
        spaces = np.where(board == card[0])[0]
        for i in range(card[1]):
            if np.any(spaces > self.pos):
                self.pos = spaces[np.argmax(spaces > self.pos)]
            else:
                self.pos = len(board)
        print(f'Your new position is {self.pos}!')
        return 
```

Now that we can create players and a deck, let's allow the users to put in how many players there are and their respective names.


```python
def findPlayers():
    characters = []
    numChars = int(input('How many players (2-4)? '))
    for i in range(numChars):
        name = input(f"Player {i + 1} name? ")
        characters.append(Player(name))
    return characters
```

Let's include some game playing instructions for our players!


```python
def instructions():
    print("Welcome to Candyland. Reach the last space of the board before anybody else does.")
    print("Draw a card to advance.")
    print("Press ENTER to start each player's turn")
    print()
    print('----------------------------------------------------------------')
    print()
```

Alrighty! We have all the basics for our game! Let's put them all together into one `main()` function. Let's call our `instructions` function and then build our deck and board. Then we can find our players! Now let's work through turns. Let's tell our player it's their turn, have them draw a card, and then print the card. Then our player can use their move method to go where their card tells them to. Let's check if they made it to the end of the board, and if it is, then tell our player they won!


```python
def main():
    instructions()
    deck = Deck()
    board = createBoard()
    characters = findPlayers()
    while characters:
        for character in characters:
            print()
            print(f'{character.name}: It is your turn')
            input()
            card = deck.drawCard()
            character.printCard(card)
            character.move(card)
            if character.pos == len(board):
                print(f'Congratulations {character.name}, you won!')
                return 
```

Have fun playing! Call the `main()` function below to get started!


```python
main()
```
