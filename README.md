# Codex-TicTacToe
#I created a tic tac toe game by copying the basic rules of Tic Tac Toe and giving it to OpenAI's codex. I did not write the code myself, the AI did. 

#This is what I told it
'''
Step 1: Set Up the Tic-Tac-Toe Game Board With Tkinter
Ensure the Right Tkinter Version
Create a Class to Represent the Game Board
Step 2: Set Up the Tic-Tac-Toe Game Logic in Python
Define Classes for the Players and Their Moves
Create a Class to Represent the Game Logic
Set Up the Abstract Game Board
Figure Out the Winning Combinations
Step 3: Process the Players’ Moves on the Game’s Logic
Validate Players’ Moves
Process Players’ Moves to Find a Winner
Check for Tied Games
Toggle Players Between Turns
Step 4: Process Players’ Moves on the Game Board
Handle a Player’s Move Event
Update the Game Board to Reflect the Game State
Run Your Tic-Tac-Toe Game for the First Time
Step 5: Provide Options to Play Again and Exit the Game
Build the Game’s Main Menu
Implement the Play Again Option
'''

#This is the code the AI wrote.

import tkinter as tk
from tkinter import messagebox

class TicTacToe:
    def __init__(self):
        self.root = tk.Tk()
        self.root.title("Tic Tac Toe")
        self.root.resizable(0, 0)
        self.root.wm_attributes("-topmost", 1)
        self.board = tk.Canvas(self.root, width=300, height=300, bd=8, highlightthickness=8, bg="black")
        self.board.pack()
        self.board.bind("<Button-1>", self.callback)
        self.turn = 1
        self.state = [[0, 0, 0], [0, 0, 0], [0, 0, 0]]
        self.buttons = []
        for i in range(3):
            self.buttons.append([])
            for j in range(3):
                self.buttons[i].append(self.board.create_rectangle(i * 100, j * 100, (i + 1) * 100, (j + 1) * 100, fill="white"))
        self.root.mainloop()

    def callback(self, event):
        if self.turn == 1:
            self.draw_x(event.x, event.y)
        else:
            self.draw_o(event.x, event.y)

    def draw_x(self, x, y):
        if self.state[int(x / 100)][int(y / 100)] == 0:
            self.board.create_line(x - 20, y - 20, x + 20, y + 20, fill="red", width=4)
            self.board.create_line(x + 20, y - 20, x - 20, y + 20, fill="red", width=4)
            self.state[int(x / 100)][int(y / 100)] = 1
            self.turn = 2
            self.check_winner()

    def draw_o(self, x, y):
        if self.state[int(x / 100)][int(y / 100)] == 0:
            self.board.create_oval(x - 20, y - 20, x + 20, y + 20, fill="blue")
            self.state[int(x / 100)][int(y / 100)] = 2
            self.turn = 1
            self.check_winner()

    def check_winner(self):
        for i in range(3):
            if self.state[i][0] != 0 and self.state[i][0] == self.state[i][1] and self.state[i][1] == self.state[i][2]:
                self.winner(self.state[i][0])
        for i in range(3):
            if self.state[0][i] != 0 and self.state[0][i] == self.state[1][i] and self.state[1][i] == self.state[2][i]:
                self.winner(self.state[0][i])
        if self.state[0][0] != 0 and self.state[0][0] == self.state[1][1] and self.state[1][1] == self.state[2][2]:
            self.winner(self.state[0][0])
        if self.state[0][2] != 0 and self.state[0][2] == self.state[1][1] and self.state[1][1] == self.state[2][0]:
            self.winner(self.state[0][2])

    def winner(self, player):
        if player == 1:
            messagebox.showinfo("Winner", "X wins!")
        else:
            messagebox.showinfo("Winner", "O wins!")
        self.root.destroy()

if __name__ == "__main__":
    TicTacToe()
