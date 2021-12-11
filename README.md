# A Way Home
# Bor Makuach
# Dec 5th, 2021

import random

# Adds values to Player(s)
class Player:
    def __init__(self, name, hp=24, power=random.choice(range(1, 20))):
        self.name = name
        self.hp = hp
        self.power = power
        
    def __repr__(self):
        return self.name + ": " + str(self.hp) + "hp "
    
# Adds values to Enemy(s)
class Enemy:
    def __init__(self, name, hp, power):
        self.name = name
        self.hp = hp
        self.power = power
        
    def __repr__(self):
        return self.name + ": " + str(self.hp) + "hp "

# Adds values to Situations(s)
class Situation:
    def __init__(self, name, power):
        self.name = name
        self.power = power
        
    def __repr__(self):
        return self.name + " has a power of " + self.power

class Heal:
    def __init__(self, name, hp):
        self.name = name
        self.hp = hp 
        
    def __repr__(self):
        return self.name + " gives " + self.hp + "hp"   
    
# Player Turn 
def playerturn(player, enemy):
        damage = player.power
        enemy.hp -= damage
        return player.name + " attacks and does " + str(damage) + " damage " + "\n" + str(enemy) + "\n"
        
# Enemy Turn
def enemyturn(player, enemy):
        damage = enemy.power
        player.hp -= damage
        return enemy.name + " attacks and does " + str(damage) + " damage " + "\n" + str(player) + "\n"
 
def item_heal(player, heal_item):
    player.hp += heal_item.hp
    return "You find " + heal_item.name + "...Awards " + str(heal_item.hp) + "hp \n" + player.name + " " + str(player.hp) + "hp" 
          
# Battle logic
def battle(player, enemy): 
    enemy_full_health = enemy.hp
    print("\n" + player.name + ", looks like there is something coming... It's a... \n" + enemy.name + "\nYou must fight it!\n") 
    battle = True
    while battle == True:
        attack = input("Attack (enter y): ")
        x = random.choice(range(1, 15))
        award = x
        if attack == "y":
            print(playerturn(player, enemy))
            if enemy.hp <= 0:
                print("You have Won! \nYou are awarded " + str(award) + "hp \n")
                enemy.hp = enemy_full_health
                battle = False
            else:
                print(enemyturn(player, enemy))
                if player.hp <= 0:
                    print("You were killed")
                    battle = False
                    
    
# Event logic          
def event(player, situation): 
    print("There is a fork do you want to Go Right (y) or Go Left (n)\n") 
    alive = True
    while alive == True:
        choice = input("Go Left or Go Right (Enter L/R)\n")
        right_answer = random.choice([["l", "L"], ["r", "R"]])
        if choice == right_answer:
            player.hp += situation.power
            print("Wise choice you are arwarded " + str(situation.power) + "hp \n" + player.name + ": " + str(player.hp) + "hp \n")
            alive = False
        if choice != right_answer:
            player.hp -= situation.power
            print("You ran into " + situation.name + "\nYou take " + str(situation.power) + " damage\n" + player.name + ": " + str(player.hp) + "hp")
            alive = False


power = random.choice(range(1, 10))

# Enemies
trex = Enemy("T-Rex", 50, power)
slime = Enemy("Slime", 5, power)
dragon = Enemy("Dragon", 30, power)
bear = Enemy("Bear", 24, power)
cat = Enemy("Cat", 10, power)
fish = Enemy("Fish", 5, power)
big_fish = Enemy("Big Fish", 18, power)

enemies = [slime, dragon, bear, cat, fish, big_fish]
enemy = random.choice(enemies) 


# Situations
rockslide = Situation("Rock Slide", power)
fallen_tree = Situation("Fallen Tree", power)
avalanche = Situation("Avelanche", power)
tsunami = Situation("Tsumani", power)
tornado = Situation("Tornado", power)
earthquake = Situation("Earthquake", power)
hurricane = Situation("Hurricane", power)
lightning = Situation("Lightning", power)
sandstorm = Situation("Sandstorm", power)
tarpit = Situation("Tar Pit", power)
quicksand = Situation("Quicksand", power)
meteors = Situation("Meteor Shower", power)
wildfire = Situation("Wild Fire", power)

situations = [rockslide, fallen_tree, avalanche, tsunami, tornado, earthquake, hurricane, lightning, sandstorm, tarpit, quicksand, meteors, wildfire]
situation = random.choice(situations)

# Heal Items
bandage = Heal("Bandage", 7)
berries = Heal("Berries", 5)
med_kit = Heal("Med Kit", 15)

items = [bandage, berries, med_kit]
item = random.choice(items)

# Asks Player Name
player1 = input("Enter Your Name: ")
player1 = Player(player1)

level = 0

def fork():
    print("There is a fork up ahead Go Right or Go Left")
    choice = input("Enter R/L: ")
    if choice == ["R", "r"]:
        print("You chose to go Right")
        
    if choice == ["L", "l"]:
        print("You chose to go Left")
    

class Game:
    level = 0
    if level == 0:
        print("You've been woken up by the sound of waves... \nWhere am I?? What happened??\nI remember having a good night on the cruise but after that nothing..")
        print('You start exploring...\n\n...\n\nYou notice a path \nBefore entering you see a sign\n"BEWARE THE DANGERS OF THE ISLAND"')
        a = input("Continue Along The Path? (Enter y): ")
        if a == "y" or a == "Y":
            print("You notice something written on the back of the sign\n'Along the path you will encounter various enemies I've left behind bangdages and med kits for your journey \n The berris along the path taste bad but will heal you Good Luck \n P.S Left=good Right = Bad'")
            path = True 
    
        
    while path == True:
        if level == 2:
            fork()
        if level == 5:
            print("There appears to be a house not to far away..")       
        if level == 10:
            path = False
            print("You've finally made it to the house..\n You enter and after looking around you find a radio.\nAfter traveling the island you begin to enjoy the thrills it provides do you wish to stay and make a life here or call for help?")
            stay_or_go = input("Radio Help (Enter y) Stay (Enter n)")
            if stay_or_go == "y":
                print("You radio for help and are rescued\nGame Over")
            else:
                print("You choose continue along the path")  
                path = True  
        
        if player1.hp > 0:
            a = input("Keep Moving (Enter y/n) \n")
            if a == "y":
                y = random.choice(range(1, 4))
                if y == 1:
                    event(player1, situation)
                    level += 1
                if y == 2:
                    battle(player1, enemy)
                    level += 1
                if y == 3:
                    item_heal(player1, item)
                    level += 1
                
        
            elif a != "y":
                print("Doesn't seem like you would like to move forward are you sure? ")
                b = input("(Enter y/n)")
                if b == "y":
                    path = True
                    a == "y"
                else:
                    print("You Decide To Lay Down And Give Up")
                    path = False           
        if player1.hp <= 0:
            path = False

Game     
