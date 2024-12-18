import random
import time

# Game state variables
player_name = ""
player_status = {"health": 100, "wealth": 100000, "happiness": 80, "relationship_status": "married", "career": "Entrepreneur"}
divorce_counter = 0
terrorist_attack = False
military_conflict = False
career_events = ["promotion", "networking success", "investor meetings", "startup success", "fired"]

def print_slow(str):
    """Function to print text slowly for dramatic effect."""
    for letter in str:
        print(letter, end='', flush=True)
        time.sleep(0.05)
    print()

def start_game():
    global player_name
    print_slow("Welcome to Life Luxe: A Day in the Fast Lane!")
    player_name = input("Enter your character's name: ")
    print_slow(f"Hello, {player_name}! Welcome to your luxury life simulation.")
    main_menu()

def main_menu():
    """Main game menu where the player can choose their daily routine or face challenges."""
    while True:
        print_slow("\nWhat would you like to do today?")
        print_slow("1. Work (Career Events)")
        print_slow("2. Leisure (Gym, Park, Family)")
        print_slow("3. Check Health and Happiness")
        print_slow("4. Check Wealth and Career Progress")
        print_slow("5. Face Challenges (Military, Terrorist Attack, Divorce)")
        print_slow("6. Exit Game")
        
        choice = input("Choose an option: ")
        
        if choice == "1":
            work_day()
        elif choice == "2":
            leisure_time()
        elif choice == "3":
            check_health_happiness()
        elif choice == "4":
            check_wealth_career()
        elif choice == "5":
            face_challenges()
        elif choice == "6":
            print_slow("Thank you for playing Life Luxe! Until next time.")
            break
        else:
            print_slow("Invalid choice. Please choose again.")

def work_day():
    """Work-related events such as career achievements, promotions, or layoffs."""
    print_slow("\nYou head to work in your luxury office. It's a busy day!")
    event = random.choice(career_events)
    
    if event == "promotion":
        print_slow("Congratulations! You received a promotion!")
        player_status["wealth"] += 20000
        player_status["happiness"] += 10
    elif event == "networking success":
        print_slow("You successfully networked with influential people. Business is booming!")
        player_status["wealth"] += 15000
        player_status["happiness"] += 8
    elif event == "investor meetings":
        print_slow("You secured funding for your startup. Your business is growing!")
        player_status["wealth"] += 50000
        player_status["happiness"] += 5
    elif event == "startup success":
        print_slow("Your startup is doing exceptionally well. You're on track to become a billionaire!")
        player_status["wealth"] += 100000
        player_status["happiness"] += 15
    elif event == "fired":
        print_slow("Oh no! You've been fired. The company is downsizing.")
        player_status["wealth"] -= 30000
        player_status["happiness"] -= 20

def leisure_time():
    """Leisure activities like gym, park jog, or spending time with family."""
    print_slow("\nIt's time to relax and unwind.")
    activity = input("What would you like to do? (1) Gym (2) Jogging in Park (3) Spend time with family: ")
    
    if activity == "1":
        print_slow("You had a great workout session. Your body feels stronger and healthier!")
        player_status["health"] += 10
        player_status["happiness"] += 5
    elif activity == "2":
        print_slow("A refreshing jog in the park. The fresh air energizes you!")
        player_status["health"] += 5
        player_status["happiness"] += 7
    elif activity == "3":
        print_slow("You spend quality time with your family. They appreciate you more.")
        player_status["happiness"] += 10
    else:
        print_slow("Invalid choice! Try again.")
        
def check_health_happiness():
    """Display health and happiness stats."""
    print_slow(f"\nCurrent Health: {player_status['health']}")
    print_slow(f"Current Happiness: {player_status['happiness']}")

def check_wealth_career():
    """Display wealth and career stats."""
    print_slow(f"\nCurrent Wealth: ${player_status['wealth']}")
    print_slow(f"Current Career: {player_status['career']}")
    print_slow(f"Relationship Status: {player_status['relationship_status']}")

def face_challenges():
    """Handle major life challenges like military conflict, terrorist attack, and divorce."""
    global military_conflict, terrorist_attack, divorce_counter
    
    challenge = random.choice(["military", "terrorist", "divorce", "nothing"])
    
    if challenge == "military":
        military_conflict = True
        print_slow("\nMilitary conflict has broken out. Your country is under attack!")
        print_slow("You must make a choice: Do you (1) fight for your country or (2) stay at home and protect your family?")
        choice = input("Choose 1 or 2: ")
        
        if choice == "1":
            result = random.choice(["win", "lose"])
            if result == "win":
                print_slow("You fought bravely and helped your country win the battle. Heroes are born!")
                player_status["happiness"] += 20
            else:
                print_slow("Your side lost. The impact on your life is severe. You are emotionally shaken.")
                player_status["health"] -= 20
                player_status["happiness"] -= 30
        elif choice == "2":
            print_slow("You decided to stay at home. While your family is safe, the emotional toll is heavy.")
            player_status["happiness"] -= 15
        else:
            print_slow("Invalid choice. You made no decision. The conflict escalates without your help.")
            player_status["health"] -= 10
            player_status["happiness"] -= 25
    
    elif challenge == "terrorist":
        terrorist_attack = True
        print_slow("\nA terrorist attack has occurred in your city. It's a dangerous situation.")
        print_slow("You have to decide: Do you (1) help the authorities or (2) protect your loved ones?")
        choice = input("Choose 1 or 2: ")
        
        if choice == "1":
            result = random.choice(["help", "failure"])
            if result == "help":
                print_slow("Your help saved lives. You're a hero!")
                player_status["happiness"] += 15
                player_status["wealth"] += 10000
            else:
                print_slow("You were too late. Many lives were lost, and you're emotionally affected.")
                player_status["health"] -= 15
                player_status["happiness"] -= 20
        elif choice == "2":
            print_slow("You stayed with your loved ones. While you’re safe, you feel guilty for not helping.")
            player_status["happiness"] -= 10
        else:
            print_slow("You hesitated and did nothing. The attack caused widespread chaos.")
            player_status["health"] -= 20
            player_status["happiness"] -= 30
    
    elif challenge == "divorce":
        divorce_counter += 1
        if divorce_counter == 1:
            print_slow("\nYour spouse has filed for divorce. Tensions have been rising for months.")
            print_slow("Do you (1) try to reconcile or (2) agree to the divorce?")
            choice = input("Choose 1 or 2: ")
            
            if choice == "1":
                result = random.choice(["reconcile", "end"])
                if result == "reconcile":
                    print_slow("You managed to reconcile and save the marriage. It’s a fresh start!")
                    player_status["happiness"] += 15
                else:
                    print_slow("Unfortunately, the divorce is final. You part ways amicably.")
                    player_status["happiness"] -= 40
                    player_status["health"] -= 10
            elif choice == "2":
                print_slow("You agreed to the divorce. It’s a painful chapter, but you’ll move forward.")
                player_status["happiness"] -= 30
                player_status["wealth"] -= 50000  # Legal costs
            else:
                print_slow("You didn’t make a decision. The divorce goes through.")
                player_status["happiness"] -= 50
                player_status["wealth"] -= 50000
        else:
            print_slow("\nThe divorce is finalized, and it’s a tough time. You need time to heal.")
            player_status["health"] -= 20
            player_status["happiness"] -= 30
    
    elif challenge == "nothing":
        print_slow("\nIt’s a calm day. No major challenges today.")

# Start the game
start_game()
