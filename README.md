# Reflex - Number Guessing Game
Powered by [reflex.dev](https://reflex.dev/) 



## Tech Stack

- Python 3.12
- Reflex 0.5.5+, currently 0.6.4
- Pandas

    BTW - I am on Ubuntu 24.04.



## Getting Started

1. Basic setup
    ```shell
    ## Update and Upgrade
    sudo apt update && sudo apt upgrade -y
    ## Install the virtualenv tool and unzip
    sudo apt install python3.12-venv unzip
    
    ## Install node.js 22
    sudo apt install nodejs -y
    ## brew install node@22
    
    ## Install the `bun` package manager for later use with Reflex
    ## If you have Node.js v20+ installed, this is not neccessary!
    # curl -fsSL https://bun.sh/install | bash
    ## activate the .bashrc to make sure `bun` is accessible
    # source ~/.bashrc
    ```
2. Create venv and give a go
    ```shell
    ## Make project directory
    mkdir reflex-game
    cd reflex-game
    ## create a venv named as '.venv'
    python3 -m venv .venv
    ## activate it
    source .venv/bin/activate
    ## list the modules in the .venv (only 'pip' itself)
    pip list
    ## Optuioally upgrade pip
    pip install --upgrade pip
    
    ## Ensure the python3 and pip are from the .venv, 
    ## if output is like "/usr/bin/", then remake the .venv
    which python3
    which pip
    ```
    Note: <font color="red">The ops below are in the Virtual Environment.</font>
    
3. Install the monster - Reflex
    ```shell
    ## This takes quite a while as many modules pop in
    pip install reflex==0.6.4
    ## check them out
    pip list
    ```
4. Give a go
    ```shell
    reflex init --template empty
    ```
    It will prompt you some templates to select with, choose '0' which represents 'empty'. 

    And the process will generate quite a few files in the project folder.
5. Install some extra python modules: pandas, numpy, etc. (please do)
    ```shell
    ## edit requirements.txt file ensuring the version of reflex == 0.6.4 (>=0.5.5)
    ## because the latest version 0.6.5 is very buggy as of November 12, 2024.
    pip install -r requirements.txt
    ```
6. Start up the Reflex App
    ```shell
    reflex run
    ```
    Eventually, you will be presented with:
    
    > App running at: http://localhost:3000 
    >
    > Backend running at: http://0.0.0.0:8000
7. Enjoy the show.



## The Game: Real-Time Number Guessing

Now let’s create for real a game with Reflex: a simple yet engaging number guessing game! This game will allow players to guess a secret number within a specified range, receiving instant feedback on their guesses.

```
import reflex as rx
import random

class GameState(rx.State):
    """The game state."""
    secret_number: int = random.randint(1, 100)
    guess: int = 0
    message: str = "I've chosen a number between 1 and 100. Can you guess it?"
    def check_guess(self):
        """Check the player's guess against the secret number."""
        if self.guess == self.secret_number:
            self.message = "Congratulations! You guessed it!"
        elif self.guess < self.secret_number:
            self.message = "Too low! Try again."
        else:
            self.message = "Too high! Try again."
def index():
    return rx.center(
        rx.vstack(
            rx.heading("Number Guessing Game"),
            rx.text(GameState.message),
            rx.input(type="number", on_change=GameState.set_guess),
            rx.button("Guess", on_click=GameState.check_guess),
            align_items="center",
        ),
        width="100%",
        height="100vh",
    )
app = rx.App()
app.add_page(index, title="Number Guessing Game")
```

**Explanation:**

**Imports:** We start by importing reflex as rx and the random module for generating our secret number.

**Game State:** The GameState class manages the game’s data:

- secret_number: This variable holds the randomly chosen number that the player needs to guess.
- guess: This variable stores the player’s current guess.
- message: This variable holds messages to guide the player, indicating whether their guess was too high, too low, or correct.

The check_guess function is an event handler triggered when the player clicks the “Guess” button. It compares the guess with the secret_number and updates the message accordingly.

**User Interface (index function):** The index function constructs the game’s visual interface:

- rx.center: Centers the game content.
- rx.vstack: Arranges elements vertically.
- rx.heading: Displays the title “Number Guessing Game”.
- rx.text: Shows the message from the GameState.
- rx.input: Provides a numeric input field for the player to enter their guess.
- rx.button: The “Guess” button triggers the check_guess function.



## Push the Project to GitHub

1. Create a empty repository on your GitHub space, named as, say `nba-data-dash`.

2. Edit the `.gitignore` file to exclude the `venv` folder.

3. Commit and Push to the repo:

   ```shell
   ## Add data files in
   git add .
   ## Commit
   git commit -m "reflex-game"
   ## channel it to master - sorry not a fan of main
   git branch -M master
   ## conenct to remote repo
   git remote add origin https://github.com/marcuszou/reflex-game.git
   ## Push the project files
   git push -u origin master
   ```

   

## License
MIT
    

