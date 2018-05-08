''' 
Tic-Tac-Toe using classes to exercize object oriented placement.
I created TicTacToe first as I'm sure many do. Used Python and classes to show an understanding of OOP. Pretty straight forward.
JCR 05/08/2018
'''
import os
import string


class Board():
	def __init__(self):
		self.clear_board()

	def clear_board(self):
		self.cells = [' '] * 9

	def check_draw(self):
		return not (" " in self.cells[0:])

	def display(self):
		''' Print out display '''
		print (" %s | %s | %s " %(
			self.cells[0] if self.cells[0] != ' ' else 1, 
			self.cells[1] if self.cells[1] != ' ' else 2,
			self.cells[2] if self.cells[2] != ' ' else 3))
		print ('-----------')
		print (" %s | %s | %s " %(
			self.cells[3] if self.cells[3] != ' ' else 4,
			self.cells[4] if self.cells[4] != ' ' else 5, 
			self.cells[5] if self.cells[5] != ' ' else 6))
		print ('-----------')
		print (" %s | %s | %s " %(
			self.cells[6] if self.cells[6] != ' ' else 7, 
			self.cells[7] if self.cells[7] != ' ' else 8, 
			self.cells[8] if self.cells[8] != ' ' else 9))

	def update_cell(self, cell_no, mark):
		if self.cells[cell_no] == " ":
			self.cells[cell_no] = mark

	def is_winner(self):
		''' Check Horozontals,Verticals, and Diagonals for a win '''
		if self.cells[0] == self.cells[1] == self.cells[2] != ' ':
			return self.cells[0]
		if self.cells[3] == self.cells[4] == self.cells[5] != ' ':
			return self.cells[3]
		if self.cells[6] == self.cells[7] == self.cells[8] != ' ':
			return self.cells[6]
		if self.cells[0] == self.cells[4] == self.cells[8] != ' ':
			return self.cells[0]
		if self.cells[2] == self.cells[4] == self.cells[6] != ' ':
			return self.cells[2]
		if self.cells[0] == self.cells[3] == self.cells[6] != ' ':
			return self.cells[0]
		if self.cells[1] == self.cells[4] == self.cells[7] != ' ':
			return self.cells[1]
		if self.cells[2] == self.cells[5] == self.cells[8] != ' ':
			return self.cells[2]

		else:
			return " "

board_instance = Board()

def print_header():
	print ("Welcome to Tic-Tac-Toe\n")

def refresh_screen():
	os.system("cls")
	print_header()
	board_instance.display()

def player_choice(mark):
	''' Asks player where to place X or O mark, checks validity, updates cell '''
	choice = -1
	while True:
		choice = int(input("\n"+(mark)+") choose 1-8   >")) -1
		if choice >8 or choice <0:
			print("Sorry, please input a number between 1-9. ")
			continue

		board_instance.update_cell(choice, mark)
		break

def if_winner(mark):
	return board_instance.is_winner() != " "

def if_play_again():
	playagain = (input("\nWould you like to play again? Yes or No? "))
	if playagain.lower() == 'yes':
		board_instance.clear_board()
		return True
	return False

while True:
	refresh_screen()
	player_choice('X')

	if if_winner('X'):
		print("'X' wins! Congratulations!")
		if not if_play_again():
			break
		continue

	if board_instance.check_draw():
		print("\nYou're both losers!\n")
		if not if_play_again():
			break
		continue

	refresh_screen()
	player_choice('O')

	if if_winner('O'):
		print("'O' wins! Congratulations!")
		if not if_play_again():
			break
		continue

	if board_instance.check_draw():
		print("\nYou're both losers!\n")
		if not if_play_again():
			break
		continue
