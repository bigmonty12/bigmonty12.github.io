---
layout: post
title: "Python for Beginners: Battleship"
date: 2020-04-27 19:55:00 -0700
categories: jekyll beginner-python
permalink: /battleship
---
# Battleship for Beginners



## Introduction
In the previous lesson, we saw the beginning steps of how to create Mario Party with Python. We saw examples of creating graphs, creating characters, and simulating dice. In this lesson, we will learn some more basic Python concepts including functions, lists, and if-else statements!

### Lists
We saw examples of lists in our Mario Party example from last week.
```
characters_list = ['Mario', 'Diddy Kong', 'Waluigi', 'Boom Boom']
```
Lists are Python objects that let us store things in a convenient location so we can find them later. It's like when you go to a store with a list written down so you can remember what you need.
> Bananas, OJ, yogurt, Chewbacca onesie pajamas

One nice thing about lists is that you are able to add and remove things from them. Adding to a list is also known as 'appending.' 
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
build_board(10)
```




    [['O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O'],
     ['O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O'],
     ['O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O'],
     ['O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O'],
     ['O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O'],
     ['O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O'],
     ['O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O'],
     ['O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O'],
     ['O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O'],
     ['O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O']]



We built and printed our board but it doesn't look very pretty. Let's write another function so that we get rid of the brackets, quotes, and commas. 

The * symbol is use to print the list elements in a single line with a space. We use a for loop here to print each list element.

```python
def print_board(board):
    for b in board:
        print(*b)
```

```python
board = build_board(7)
print_board(board)
```

    O O O O O O O
    O O O O O O O
    O O O O O O O
    O O O O O O O
    O O O O O O O
    O O O O O O O
    O O O O O O O


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
ship = build_ship(5); ship
```




    [(0, 0), (0, 1), (0, 2), (0, 3)]



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

    Row: 2
    Col: 3





    (1, 2)



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

    Row: 1
    Col: 2
    LOL miss!
    O X O O O O O
    O O O O O O O
    O O O O O O O
    O O O O O O O
    O O O O O O O
    O O O O O O O
    O O O O O O O


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

    Welcome to Battleship!
    There is a battleship hidden in this board. Enter your row and column guesses to sink it!
    Row: 1
    Col: 5
    LOL miss!
    O O O O O
    O O O O O
    O O O O O
    O O O O O
    O O O O O
    Row: 1
    Col: 1
    LOL miss!
    O O O O O
    O O O O O
    O O O O O
    O O O O O
    O O O O O
    Row: 4
    Col: 2
    LOL miss!
    O O O O O
    O O O O O
    O O O O O
    O O O O O
    O O O O O
    Row: 5
    Col: 1
    LOL miss!
    O O O O O
    O O O O O
    O O O O O
    O O O O O
    O O O O O
    Row: 2
    Col: 3
    LOL miss!
    O O O O O
    O O O O O
    O O O O O
    O O O O O
    O O O O O
    Row: 5
    Col: 5
    LOL miss!
    O O O O O
    O O O O O
    O O O O O
    O O O O O
    O O O O O
    Row: 4
    Col: 4
    LOL miss!
    O O O O O
    O O O O O
    O O O O O
    O O O O O
    O O O O O
    Row: 3
    Col: 3
    LOL miss!
    O O O O O
    O O O O O
    O O O O O
    O O O O O
    O O O O O
    Row: 1
    Col: 3
    LOL miss!
    O O O O O
    O O O O O
    O O O O O
    O O O O O
    O O O O O
    Row: 3
    Col: 1
    LOL miss!
    O O O O O
    O O O O O
    O O O O O
    O O O O O
    O O O O O
    Row: 5
    Col: 3
    LOL miss!
    O O O O O
    O O O O O
    O O O O O
    O O O O O
    O O O O O
    Row: 2
    Col: 2
    You hit my battleship!
    O O O O O
    O X O O O
    O O O O O
    O O O O O
    O O O O O
    Row: 3
    Col: 2
    LOL miss!
    O O O O O
    O X O O O
    O O O O O
    O O O O O
    O O O O O
    Row: 2
    Col: 3
    You already guessed that, silly!
    O O O O O
    O X O O O
    O O O O O
    O O O O O
    O O O O O
    Row: 1
    Col: 2
    You hit my battleship!
    O X O O O
    O X O O O
    O O O O O
    O O O O O
    O O O O O
    You sunk my battleship!

