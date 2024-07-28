import random

# List of words to choose from
WORDS = ['python', 'hangman', 'challenge', 'programming', 'development', 'software']

def choose_word():
    """Randomly select a word from the WORDS list."""
    return random.choice(WORDS)

def display_word(word, guessed_letters):
    """Display the word with guessed letters and underscores for unguessed letters."""
    return ' '.join(letter if letter in guessed_letters else '_' for letter in word)

def hangman():
    word = choose_word()
    guessed_letters = set()
    attempts_remaining = 6  # Number of allowed incorrect attempts
    
    print("Welcome to Hangman!")
    print("Try to guess the word!")
    
    while attempts_remaining > 0:
        word_display = display_word(word, guessed_letters)
        print("\nCurrent word: ", word_display)
        print(f"Attempts remaining: {attempts_remaining}")
        print(f"Guessed letters: {', '.join(sorted(guessed_letters))}")
        
        guess = input("Guess a letter: ").lower()
        
        if len(guess) != 1 or not guess.isalpha():
            print("Please enter a single alphabetic character.")
            continue
        
        if guess in guessed_letters:
            print("You already guessed that letter.")
            continue
        
        guessed_letters.add(guess)
        
        if guess in word:
            print("Good guess!")
        else:
            print("Incorrect guess.")
            attempts_remaining -= 1
        
        if '_' not in display_word(word, guessed_letters):
            print("\nCongratulations! You've guessed the word:", word)
            break
    else:
        print("\nGame over! The word was:", word)

if __name__ == "__main__":
    hangman()
