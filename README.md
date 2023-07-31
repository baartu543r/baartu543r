import random

class Player:
    def __init__(self, name, health, attack):
        self.name = name
        self.health = health
        self.attack = attack

    def take_damage(self, damage):
        self.health -= damage

    def is_alive(self):
        return self.health > 0

    def attack_enemy(self, enemy):
        damage = random.randint(1, self.attack)
        enemy.take_damage(damage)
        print(f"{self.name} attacks {enemy.name} for {damage} damage!")

class Enemy:
    def __init__(self, name, health, attack):
        self.name = name
        self.health = health
        self.attack = attack

    def take_damage(self, damage):
        self.health -= damage

    def is_alive(self):
        return self.health > 0

    def attack_player(self, player):
        damage = random.randint(1, self.attack)
        player.take_damage(damage)
        print(f"{self.name} attacks {player.name} for {damage} damage!")

def main():
    player_name = input("Enter your name: ")
    player = Player(player_name, health=100, attack=20)

    enemies = [
        Enemy("Goblin", health=50, attack=10),
        Enemy("Orc", health=70, attack=15),
        Enemy("Dragon", health=150, attack=25)
    ]

    level = 1

    while level <= len(enemies):
        print(f"\nLevel {level}")
        current_enemy = enemies[level - 1]

        print(f"You encounter a {current_enemy.name}!")
        while player.is_alive() and current_enemy.is_alive():
            print(f"\n{player.name} - Health: {player.health}")
            print(f"{current_enemy.name} - Health: {current_enemy.health}")
            print("1. Attack")
            print("2. Run")
            choice = input("Enter your choice (1/2): ")

            if choice == "1":
                player.attack_enemy(current_enemy)
                if not current_enemy.is_alive():
                    print(f"You defeated the {current_enemy.name}!")
            elif choice == "2":
                print(f"{player.name} runs away from the {current_enemy.name}.")
                break
            else:
                print("Invalid choice. Try again.")

            if current_enemy.is_alive():
                current_enemy.attack_player(player)

        if not player.is_alive():
            print("Game Over! You were defeated.")
            break
        else:
            print("Level complete! Proceed to the next level.")
            level += 1

    if player.is_alive():
        print("Congratulations! You completed all levels and won the game!")

if __name__ == "__main__":
    main()
