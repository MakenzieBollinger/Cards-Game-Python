# Cards-Game-Python

import random

NAMES = ["2", "3", "4", "5", "6", "7", "8", "9", "10", "Jack", "Queen", "King", "Ace"]
SUITS = ["Clubs", "Diamonds", "Hearts", "Spades"]

class Card:
	def __init__(self, suit, name):
		self.name = name
		self.suit = suit
		self.value = NAMES.index(name)

class Deck:
	def __init__(self):
		self.cards = []
		for suit in SUITS:
			for name in NAMES:
				self.cards.append(Card(suit, name))
		self.shuffle()

	def shuffle(self):
		random.shuffle(self.cards)

class Player:
	def __init__(self, name, deck):
		self.name = name
		self.deck = deck

	def drawCard(self):
		return self.deck.cards.pop()

	def getDeckSize(self):
		return len(self.deck.cards)

class Game:
	def __init__(self, playerName):
		d = Deck()
		self.player = Player(playerName, d)
		self.turn = 1
		self.score = 0

	def startGame(self):
		print "Welcome to Higher or Lower!"
		self.lastPlayed = self.player.drawCard()
		while self.player.getDeckSize() > 0:
			self.playTurn()

	def playTurn(self):

		print "Turn", self.turn,". Last card drawn: ", self.lastPlayed.name, "of", self.lastPlayed.suit
		print "Current score is: ", self.score
		res = raw_input("Do you think the next card will be higher or lower? (h/l) ")
		card = self.player.drawCard()
		if res == "h":
			if card.value >= self.lastPlayed.value:
				print "Correct!"
				self.score += 1
			else:
				print "Incorrect."
		elif res == "l":
			if card.value <= self.lastPlayed.value:
				print "Correct!"
				self.score += 1
			else:
				print "Incorrect."

		self.lastPlayed = card
		self.turn += 1





g = Game("Makenzie")
g.startGame()

