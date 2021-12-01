# Final-Project
class Player:
    def __init__(self, name, health, power):
        self.name = name
        self.health = health
        self.power = power
    
    def __repr__(self, name, health, power):
        return "Name : " + self.name + "Health: " + self.health + "Power: " + self.power



class Enemy:
    def __init__(self, enemy, health, power):
        self.enemy = enemy
        self.health = health
        self.power = power
    
    def __repr__(self, enemy, health, power):
        return player.name + ", You have run into " + str(enemy) + ". Health: " + self.health + ". Power: " + self.power

class Situation:
    def __init__(self, situation):
        self.situation = situation
    
    def __repr__(self, situation, player.name):
        return "You've run into " + self.situation + "what do you want to do?"

class Narriator:
    def __init__(self, player1)
        self.player1 = player1
    
    if player.health = 0:
        print("You have died try again") 
        level == 0
