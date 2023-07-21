# Build_a_Tic_Tac_Toe_Game
Build a Tic-Tac-Toe Game With Python and Tkinter

Doyou remember playing Tic Tac Toe as a child? It’s a simple game that can be played on a piece of paper with just a pen or pencil. But did you know that you can also create a Tic Tac Toe game using Python’s Tkinter library? In this article, we’ll walk through the process of creating a Tic Tac Toe game using Tkinter. By the end of this article, you’ll have a basic understanding of how to create a simple game using a GUI framework, and you’ll have a fun game to play with your friends and family!

Import Libraries and Modules:

The code begins by importing the required modules and libraries, namely tkinter and messagebox modules, which are needed for creating the user interface and message prompts.

Create Window and Board:

The tk.Tk() function is used to create the main window of the game. The create_board() function is used to create the 3x3 Tic Tac Toe board using the tk.Button() method.

Initialize Variables:

The game variables are initialized, including the board list, which stores the state of the game board, and current_player variable, which tracks the current player.

Handle Button Clicks:

The handle_click() function is called whenever a button is clicked on the game board. It updates the game board with the current player's move, changes the current player to the next one, and updates the button text accordingly.

Check for Winner or Tie:

The check_for_winner() function is called after every button click to check whether there is a winner or a tie. It checks the game board for winning combinations, including rows, columns, and diagonals, and returns the winner or "tie" if no winner is found.

Declare Winner and Restart Game:

Run the Game:

The window.mainloop() function is called to start the game and runs the window until the user closes the window or ends the game.

----------------------------------------------------------: Complete Code :-------------------------------------------------------------------------------

import tkinter as tk
from tkinter import messagebox

window = tk.Tk()
window.title("Tic Tac Toe")

# Create board
def create_board():
    for i in range(3):
        for j in range(3):
            button = tk.Button(window, text="", font=("Arial", 50), height=2, width=6, bg="lightblue", command=lambda row=i, col=j: handle_click(row, col))
            button.grid(row=i, column=j, sticky="nsew")

create_board()

# Initialize variables
board = [[0, 0, 0], [0, 0, 0], [0, 0, 0]]
current_player = 1

# Handle button clicks
def handle_click(row, col):
    global current_player

    if board[row][col] == 0:
        if current_player == 1:
            board[row][col] = "X"
            current_player = 2
        else:
            board[row][col] = "O"
            current_player = 1

        button = window.grid_slaves(row=row, column=col)[0]
        button.config(text=board[row][col])

        check_for_winner()

# Check for a winner or a tie
def check_for_winner():
    winner = None

    # Check rows
    for row in board:
        if row.count(row[0]) == len(row) and row[0] != 0:
            winner = row[0]
            break

    # Check columns
    for col in range(len(board)):
        if board[0][col] == board[1][col] == board[2][col] and board[0][col] != 0:
            winner = board[0][col]
            break

    # Check diagonals
    if board[0][0] == board[1][1] == board[2][2] and board[0][0] != 0:
        winner = board[0][0]
    elif board[0][2] == board[1][1] == board[2][0] and board[0][2] != 0:
        winner = board[0][2]

    if all([all(row) for row in board]) and winner is None:
        winner = "tie"

    if winner:
        declare_winner(winner)

# Declare the winner and ask to restart the game
def declare_winner(winner):
    if winner == "tie":
        message = "It's a tie!"
    else:
        message = f"Player {winner} wins!"


    answer = messagebox.askyesno("Game Over", message + " Do you want to restart the game?")

    if answer:
        global board
        board = [[0, 0, 0], [0, 0, 0], [0, 0, 0]]

        for i in range(3):
            for j in range(3):
                button = window.grid_slaves(row=i, column=j)[0]
                button.config(text="")

        global current_player
        current_player = 1
    else:
        window.quit()

window.mainloop()
