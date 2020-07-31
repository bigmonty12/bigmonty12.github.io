---
layout: single
title: "Python for Beginners: Chutes and Ladders"
categories: games beginner-python
permalink: /chutesAndLadders
---
Chutes and Ladders. I love the simplicity of it. You spin a wheel, move that number of spaces, and occassionally slide down a chute or climb a ladder. It's fun for everyone! Today we're going to build off of the last [lesson](https://bigmonty12.github.io/candyland) and continue learning about classes.

![Chutes&Ladders](https://m.media-amazon.com/images/I/91bHa8umU7L._AC_SS350_.jpg)

Developed by:
    - Austin Montgomery
Date: 15 July 2020

## Introduction

We will see dictionaries and classes again today. It will be mostly review, but we will learn a bit more about class methods.

### Dictionaries

As a reminder, dictionaries are similar to lists. Both are used to store different objects. The difference is that dictionaries allow us to assign object to other objects. We usually refer to these as keys and values. A key is a singular object which can be associated with multiple values. A key can even be associated with a list!
```
teams = {'red': ['49ers', 'Reds', 'Hawks'], 'blue': ['Mavericks', 'Wizards'], 'silver': 'Spurs'}
```
If we want to know which teams are red, we simply type:
```
teams['red']
```
And we get our result: 
```
[49ers, 'Reds', 'Hawks']
```
![Hawks](https://upload.wikimedia.org/wikipedia/en/2/24/Atlanta_Hawks_logo.svg)

Dictionaries also gave the built in `get()` method which is a different way to get a key's value(s) than the previously demonstrated square bracket notation. 
```
teams.get('silver')
```
Which results in:
```
Spurs
```

### Classes

To review, classes are a way to combine both data and functions. It takes some time to get get used to the idea, so go back and review the previous lesson if need be. I like to use classes when I have objects which are going to be very similar but have different background details. They are also useful for making code more readable and streamlined. Let's see what a `Doctor` class would look like.
```
class Doctor():

    def __init__(self, name, specialty, pay):
        self.name = name
        self.specialty = specialty
        self.pay = pay
    
    def printDoctor(self):
        print(f'{self.name} works in {self.specialty} and makes {self.pay} dollars a year.')
```
Now let's put in the information of our favorite doctor and then use the `printDoctor()` method to learn about them!
```
Austin = Doctor('Austin', "Surgery", 900000)
Austin.printDoctor()
```
And we see:
```
Austin works in Surgery and makes 900000 dollars a year.
```
![Surgeon](https://www.drugwatch.com/wp-content/uploads/xDW-hernia-surgery-money-TP-edit-720x405-352x0-c-default.jpg.pagespeed.ic.5oNHbU704S.jpg)

### Chutes and Ladders

Now that we've reviewed, let's get working on our game!

First, we need to import the libraries we will be using. Today, we only need to import `random` (which we will use to get random numbers from spinning the wheel)


```python
import random
```

I am going to go ahead and figure out where I'm going to put my chutes and ladders. I'm going to use dictionaries to store the board positions. I looked up the actual board positions for these but feel free to put your chutes and ladders anywhere! My board is going to only have 100 spaces as well so remember to consider the length of your board when deciding these positions


```python
ladders = {1: 38, 4: 14, 9: 31, 21: 42, 28: 84, 36: 44, 51: 67, 71: 91, 80: 100}
```

Essentially, what's going to happen is in our `main()` function, we are going to check to see if the space we land on is in our dictionaries. That space will be the key (the first number). If that key is present, then we will `get()` the value and move to that new space. It will make more sense later on.


```python
chutes = {16: 6, 48: 26, 49: 11, 56: 53, 62: 19, 64: 60, 87: 24, 93: 73, 95: 75, 98: 78}
```

Next, we are going to create our `Player` class! When I create a class, I try to think of everything that class will need to be able to do, as well as what information I will need to remember for each class object. So what do we want our players to be able to do? 

Obviously, it's important for our players to be able to move, which means we have to keep track of each player's position. So we will add a variable `self.pos` and set it to 0 to start the game. A player should also be able to spin the wheel! Spinning the wheel is a random (or at least it should be!) process. We will use `random.randint(1, 6)` to get a random number between 1 and 6. Then we will add that value to our previously created `self.pos` variable. Now, we want to be verbose so the player knows what's happening. We use a print statement to tell the player what number they spun and their new position! But to keep track of each player, we better give each player a name! When we first create our player, the user can pass in the name of the player into the class function. This looks like:
```
LarryBird = Player('Larry Bird')
```
![Larry Bird](https://www.gannett-cdn.com/-mm-/adc7a8739eced7c2e4b77248ac1e5c1b813137dc/c=0-31-1236-1679/local/-/media/2016/12/07/USATODAY/USATODAY/636167218520509437-AP-C01-BIRDPLAY-07-1116641.JPG?width=300&height=400&fit=crop&format=pjpg&auto=webp)

Now `'Larry Bird'` is saved in the `self.name` variable and can be used for future use.

Two additional class methods I am going to create are `climb_ladder(ladders)` and `slide_down(chutes)` so each player knows how to naviagate the chutes and ladders. Each method is passed its respective dictionary of positions. We now see the `dict.get()` method in action. The key's value is saved as the player's new position (`self.pos`).


```python
class Player:
    def __init__(self, name):
        self.name = name
        self.pos = 0
        
    def spin_wheel(self):
        d = random.randint(1, 6)
        self.pos += d
        print(f'{self.name}: Move forward {d} space(s)')
        print(f'{self.name}: Your position is {self.pos}')
        
    def climb_ladder(self, ladders):
        self.pos = ladders.get(self.pos)
        print('Yay! You landed on a ladder!')
        print(f'{self.name}: Your new position is {self.pos}')
        
    def slide_down(self, chutes):
        self.pos = chutes.get(self.pos)
        print('Oh no! You landed on a chute!')
        print(f'{self.name}: Your new position is {self.pos}')
```

This next function is more of a housekeeping function. At the beginning of the game, we need to figure out how many players there are and each player's name. We allow the users to answer `'How many players?'` with the `input()` function and then we convert their response from a string into in integer with `int()`. Then we use a for loop so each player can `input()` their name. We pass that name to the `Player` class and `append` that player to our already initialized `characters` list. 


```python
def findCharacters():
    characters = []
    numChars = int(input('How many players (2-4)? '))
    for i in range(numChars):
        name = input(f"Player {i + 1} name? ")
        characters.append(Player(name))
    return characters
```

Our `instructions()` method is simply a series of `print()` statements so the players know how to play. Customize it however you would like!


```python
def instructions():
    print("Welcome to chutes and ladders. Reach the last space of the board before anybody else does.")
    print("Ladders will help you to the top of the board while chutes will hurt you")
    print("Press ENTER to start each player's turn")
    print()
    print('----------------------------------------------------------------')
    print()
```

We finally come to our `main()` function, where we can put together all our previous work. First thing I want to do is call `instructions()` so our player's know what they're getting themselves into. The next step is to create our list of characters with `findCharacters()`. 

Now, for the gameplay. I use a `while` statement so the function runs however long I want it to. Then we loop through our `characters` list so each player can have a turn. The first `print()` statement is to just give some white space between each players turn. Our next `print()` statement tells the players whose turn it is. I want there to be a little bit of interaction, so I use `input()` to make the player press ENTER. Otherwise, the game would simulate all the way to the end without anybody doing anything. After the player presses ENTER, their character uses the `spin_wheel()` method. After the player moves, we check if their new position is in our `ladders` or `chutes` dictionaries. If it is, then we use the correct `climb_ladder()` or `slide_down()` method. Finally, if the character reaches a position >= 100, then they win. The game is over and we `return` so the program stops running!


```python
def main():
    instructions()
    characters = findCharacters()
    while characters:
        for character in characters:
            print()
            print(f'{character.name}: It is your turn')
            input('Press ENTER to continue')
            character.spin_wheel()
            if character.pos in ladders:
                character.climb_ladder(ladders)
            if character.pos in chutes:
                character.slide_down(chutes)
            if character.pos >= 100:
                print(f'Congratulations {character.name}! You won!')
                return
                
```

I hope you have found this program fairly intuitive! Run the `main()` function below to play with your friends (or by yourself)!


```python
main()
```
