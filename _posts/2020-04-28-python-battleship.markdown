---
layout: post
title: "Python for Beginners: Battleship"
date: 2020-04-27 19:55:00 -0700
categories: jekyll beginner-python
permalink: /battleship
---
# Python for Beginners



# Battleship for Beginners
![battleship](https://www.ultraboardgames.com/battleship/gfx/banner3.jpg)

Developed by:
    - Austin Montgomery
    - Avery Smith
Date: 29 April 2020

## Introduction
In Avery's previous lesson, we saw the beginning steps of how to create Mario Party with Python. We saw examples of creating graphs, creating characters, and simulating dice. In this lesson, we will learn some more basic Python concepts including functions, lists, and if-else statements!

### Lists
We saw examples of lists in our Mario Party example from last week.
```
characters_list = ['Mario', 'Diddy Kong', 'Waluigi', 'Boom Boom']
```
Lists are Python objects that let us store things in a convenient location so we can find them later. It's like when you go to a store with a list written down so you can remember what you need.
> Bananas, OJ, yogurt, Chewbacca onesie pajamas

![Chewbacca](https://thumbor.forbes.com/thumbor/711x474/https://specials-images.forbesimg.com/dam/imageserve/958761228/960x0.jpg?fit=scale)One nice thing about lists is that you are able to add and remove things from them. Adding to a list is also known as 'appending.' 
```
characters_list.append('Luigi')
```
When you append to a list, the thing you are appending gets added to the last element of the list. Removing something from a list works the same way.
```
characters_list.remove('Boom Boom')
```
Lists also let you find specific elements within them. Suppose we had forgotten which character was second in our list (Remember that Python is 0-indexed, meaning that the first index is 0. So our second character will have an index of 1). We could type:
```
characters_list[1]
```
and we would see that it was Diddy Kong!
#### Creating lists
We can manually add elements to our list like we did with our character_list but sometimes that takes too long or we don't know exactly what will go into our lists. We are able to fix that problem by using 'for loops' and 'list comprehension.' We will see an example of list comprehension later on but we will skip the details of it for now.

### If-else statements
If-else statements are exactly what they say they are. If something is true, do this. If not, then do that.
```
if 'Mario' in characters_list:
    print("Plumber detected")
else:
    print("How can this be Mario Party without Mario?!?")
```
Sometimes we have more than two possible conditions. In these situations, we can use an 'elif' (combining else and if). Let's say that you ask your friend who their favorite Mario Party character is. Your response to them will depend on their favorite character. 
```
if friend_favorite == 'Mario':
    print('Boring')
elif friend_favorite == 'Bowser':
    print('But he is the bad guy!')
else:
    print('Cool')
```
Elif isn't used that often but it's good to understand how to think about conditions like these.


### Functions
Sometimes we find ourselves writing the same code over and over again. A good rule of thumb is that if you ever write the same code 3 times or 3more, it's time to write a function.
#### What is a function?
A function is a chunk of code that runs when you tell it to. It breaks your program into smaller chunks and makes it more organized.
#### How do I build a function?
When you build a function you must first define it; what will the function be named? This is done by typing `def ` followed by your chosen function name, parentheses, and a colon.
```
def random_character():
```
After defining you function, you can put in the chunk of code you want to run each time you call the function.
```
def random_character():
    character_list = ['Mario', 'Luigi', 'Peach', 'Bowser']
    random_num = random.randint(0, len(character_list) - 1)
    character = character_list[random_num] # Example of list indexing
    return character
```
Now we have a function that will give us a random character anytime we call it.
![Characters](data:image/jpeg;base64,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)
#### How do I call a function?
A function is called by simply typing the function's name with the associated parentheses. The result of the function (in the above case, character) can also be assigned to a new variable if the result is needed for later.
```
random_character()
# or
new_character = random_character()
```
#### What are function parameters?
Function parameters are things that are 'passed into' a function. These parameters are typed in the parentheses when defining and calling a function. Let's say that instead of having the same character_list every time in our random_character function, we want to be able to select from our original list. We will add a parameter to the function so an outside list can be used.
```
def random_character(char_list):
    random_num = random.randint(0, len(char_list) - 1)
    character = char_list[random_num]
    return character
    
new_character = random_character(['Mario', 'Diddy Kong', 'Waluigi', 'Boom Boom'])
```
Note that char_list is just a placeholder in our function. We can pass in any list as a parameter for the function and it will work. We don't need to pass in a variable already named char_list. 

### Battleship

Now that we've learned some basic Python concepts, let's get started building a game of battleship.

#### Objective
Build a game where we guess a row and column until we sink the CPU's randomly placed and randomly sized battleship.

Note: We haven't learned how some of the code works. It's okay to not understand how something works. Ask questions along the way. 

```python
# Import random package to be able to create random integers
import random
```

First item of business is we need to build a board. The cell below is our first function that we write called, you guessed it, build_board. build_board takes an integer as a parameter for however big of a square you want.

We build the board with something called list comprehension. Basically, we are saying that we want to add an element to the list however many times we tell it to. `['O' for count in range(dims)]` will add an 'O' to the list 'dims' times. This list will then be added to a list (So a list of lists) 'dims' times.

```python
# Create a square board based on dims value
def build_board(dims):
    return [['O' for count in range(dims)] for count in range(dims)]
```

```python
build_board(4)
```




    [['O', 'O', 'O', 'O'],
     ['O', 'O', 'O', 'O'],
     ['O', 'O', 'O', 'O'],
     ['O', 'O', 'O', 'O']]



We built and printed our board but it doesn't look very pretty. Let's write another function so that we get rid of the brackets, quotes, and commas. 

The * symbol is use to print the list elements in a single line with a space. We use a for loop here to print each list element.

```python
def print_board(board):
    for b in board:
        print(*b)
```

```python
board = build_board(4)
print_board(board)
```

    O O O O
    O O O O
    O O O O
    O O O O


Now we're cooking with gas! Okay, time to build a ship. We want the ship to be in a random place on the board. We also don't want to know how long the ship is. We build our ship by placing the ship coordinates into a list. Steps to build our ship:
1. Assign random length to ship
2. Randomly decide if ship will be vertical or horizontal
3. Depending on whether ship is vertical or horizontal, randomly select a row or column and then assign rest of ship positions based on length and orientation.
4. Return the list of ship coordinates

```python
# Create and return ship positional coordinates
def build_ship(dims):
    # Length of ship is random number between 2 and length of board
    len_ship = random.randint(2, dims)
    orientation = random.randint(0, 1)
    # Ship is horizontal if orientation is 0 and vertical if orientation is 1
    if orientation == 0:
        # Randomly select row and create list of selected row * length of ship
        row_ship = [random.randint(0, dims - 1)] * len_ship
        # Randomly select column of first position of ship (Hence subtracting length of ship)
        col = random.randint(0, dims - len_ship)
        # Create list of column values
        col_ship = list(range(col, col + len_ship))
        # Create positional values from row and column lists
        coords = tuple(zip(row_ship, col_ship))
    else:
        # Same as above except switch column and row
        col_ship = [random.randint(0, dims - 1)] * len_ship
        row = random.randint(0, dims - len_ship)
        row_ship = list(range(row, row + len_ship))
        coords = tuple(zip(row_ship, col_ship))
    return list(coords)
```

```python
ship = build_ship(4); ship
```




    [(1, 1), (2, 1), (3, 1)]



We built a ship! We can see our ship coordinates by calling ship after calling the function. (Remember that Python is 0-based indexed so a '0' really means the first column or row.

Now we need to create a way for us to guess the coordinates of the CPU's ship. To allow for user input, Python has a built-in function called `input()`. You can type whatever prompt you want into the input function.

It's important to know that calling `input()` will return a string, or a bunch of character types. We want our coordinates to be numbers, so we will convert them to numbers with the `int()` function (int for integer). We will also subtract 1 from our guess so we don't have to remember that Python is 0-based indexed. 

```python
def user_guess():
    # Subtract 1 to adjust for python 0-based indexing
    row = int(input('Row: ')) - 1
    col = int(input('Col: ')) - 1
    return (row, col)
```

```python
x = user_guess(); x
```

    Row: 1
    Col: 1





    (0, 0)



Great! We guessed the first row and second column and our function automatically converted it into a single pair of numbers that will work with 0-based indexing.

When we make a guess, we want the computer to know if we've already guessed it, if we hit the ship or if we missed. We will create a function `update_board` that takes four parameters: our guess, the board, the ship, and a list of all previous guesses. Then we will use if statements to update our board, guesses, and non-destroyed ship coordinates. We will also have the computer print statements so we know the results of our guess!

```python
def update_board(guess, board, ship, guesses):
    if guess in guesses:
        print('You already guessed that, silly!')
        return board
    guesses.append(guess)
    if guess in ship:
        print('You hit my battleship!')
        # Update board with 'X' signifying a hit
        board[guess[0]][guess[1]] = 'X'
        # Remove this value from ship coordinates; useful for while loop in main()
        ship.remove(guess)
        return board
    print('LOL miss!')
    return board
```

```python
# Since we haven't made any guesses yet, we pass in an empty list of guesses
guesses = [] 
our_guess = user_guess()
board = update_board(our_guess, board, ship, guesses)
print_board(board)
```

    Row: 2
    Col: 2
    You hit my battleship!
    O O O O
    O X O O
    O O O O
    O O O O


Terrific! We hit the battleship (we may have cheated by looking at the coordinates printed above lol). We made our guess and the computer told us the result and what the board now looks like! We're almost there!

Let's create one more function. When we start the game, let's have some instructions so we know what we need to do.

```python
def welcome_message():
    print('Welcome to Battleship!')
    print('There is a battleship hidden in this board. Enter your row and column guesses to sink it!')
```

```python
welcome_message()
```

    Welcome to Battleship!
    There is a battleship hidden in this board. Enter your row and column guesses to sink it!


Now we have all the steps to make our game! A good coding practice is to have a function at the end of your code that calls all your codes in one place. This makes your program easy to read and organized! The function is traditionally named `main()`.

In our main function, we have our instructions, we build a board and ship, and we create an empty list of guesses. What's that `while len(ship) > 0`, though? Well our computer has to know how long to let us guess. This is a while loop. It says that while the length of the ship's coordinates is greater than 0, keep asking for guesses (Remember we removed a ship coordinate if we guessed it correctly, so if we hit all the coordinates, the ship's list of coordinates will be empty) and printing the board. Once we've guessed all the coordinates and the length of the ship's coordinates is 0, print out a victory message!



```python
def main():
    welcome_message()
    board = build_board(5)
    ship = build_ship(5)
    guesses = []
    while len(ship) > 0:
        board = update_board(user_guess(), board, ship, guesses)
        print_board(board)
    print('You sunk my battleship!')
    return 
```

We did it! Now just call the function! Have fun playing!

```python
main()
```
