# Higher Lower Game 📊🎮

A console-based Higher Lower Game implemented in Python. Compare the number of followers of two randomly chosen Instagram accounts and guess which one has more followers.

## Features

- 🔄 Randomly selects two Instagram accounts from a provided dataset.
- 📊 Compares the number of followers between the two accounts.
- 🎯 Keeps track of the user's score.
- 🎨 Clear interface with game logo and VS symbol.

## How to Play

1. Run the Python script in a console or terminal.
2. 🔄 Compare the number of followers between two randomly chosen Instagram accounts.
3. 💡 Guess which account has more followers by typing 'A' or 'B'.
4. 📈 Receive feedback on whether the guess is correct and the current score.
5. The game continues until an incorrect guess is made.

## Code Structure

- `get_random_account()`: Function to get data from a random Instagram account.
- `format_data(account)`: Function to format account data into a printable format.
- `check_answer(guess, a_followers, b_followers)`: Function to check if the user's guess is correct.
- `game()`: Main function to initiate and control the game.

## Usage

1. Run the Python script.
2. Follow the prompts to make guesses.
3. Try to guess which Instagram account has more followers.
4. Enjoy the Higher Lower Game! 🚀

## Example

```python
from game_data import data
import random
from art import logo, vs
from replit import clear

# from game_data import data
import random
from art import logo, vs
from replit import clear

def get_random_account():
  """Get data from random account"""
  return random.choice(data)

def format_data(account):
  """Format account into printable format: name, description and country"""
  name = account["name"]
  description = account["description"]
  country = account["country"]
  # print(f'{name}: {account["follower_count"]}')
  return f"{name}, a {description}, from {country}"

def check_answer(guess, a_followers, b_followers):
  """Checks followers against user's guess 
  and returns True if they got it right.
  Or False if they got it wrong.""" 
  if a_followers > b_followers:
    return guess == "a"
  else:
    return guess == "b"


def game():
  print(logo)
  score = 0
  game_should_continue = True
  account_a = get_random_account()
  account_b = get_random_account()

  while game_should_continue:
    account_a = account_b
    account_b = get_random_account()

    while account_a == account_b:
      account_b = get_random_account()

    print(f"Compare A: {format_data(account_a)}.")
    print(vs)
    print(f"Against B: {format_data(account_b)}.")
    
    guess = input("Who has more followers? Type 'A' or 'B': ").lower()
    a_follower_count = account_a["follower_count"]
    b_follower_count = account_b["follower_count"]
    is_correct = check_answer(guess, a_follower_count, b_follower_count)

    clear()
    print(logo)
    if is_correct:
      score += 1
      print(f"You're right! Current score: {score}.")
    else:
      game_should_continue = False
      print(f"Sorry, that's wrong. Final score: {score}")

game()
