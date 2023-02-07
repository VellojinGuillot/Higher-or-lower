# Higher or Lower

import random

# Card Constants
suit_tuple = ('Spades', 'Hearts', 'Clubs', 'diamonds')
rank_tuple = ('Ace', '2', '3', '4', '5', '6', '7', '8', '9', '10', 'Jack', 'Qeen', 'King')

ncards = 8

# Pass in a deck and this function returns a random card from the deck:
def get_card(deck_list_in):
    this_card = deck_list_in.pop()# pop one off the top of the deck and return
    return this_card

# Pass in a deck and this function returns a shuffled copy of the desk: 
def shuffle(deck_list_in):
    deck_list_out = deck_list_in.copy() # Make a copy of the strating deck
    random.shuffle(deck_list_out)
    return deck_list_out

# Main code
print("Welcome to Higher or Lower.")
print("You have to choose whether the next card to be shown will be higher or lower then thecurrent card.")
print("Having the right gess will give you 20 points!; however the wrong guess will take 15 points from your basket!")
print("Don't you worry! We'll give you 50 points to start!")
print()

starting_deck_list = []
for suite in suit_tuple:
    for this_value, rank in enumerate(rank_tuple):
        card_dict = {'rank': rank, 'suit': suite, 'value': this_value + 1}
        starting_deck_list.append(card_dict)

score = 50

while True: # Play multiple games
    print()
    game_deck_list = shuffle(starting_deck_list)
    current_card_dict = get_card(game_deck_list)
    current_card_rank = current_card_dict['rank']
    current_card_value = current_card_dict['value']
    current_card_suit = current_card_dict['suit']
    print("Starting card is: ", current_card_rank + " of " + current_card_suit)

    for card_number in range(0, ncards): # Play one game of this many cards
        answer = input("Will the next card be higher or lower than the " + current_card_rank + " of " + current_card_suit + "? (Enter h or l): ")
        answer = answer.casefold() # Force lowercase
        next_card_dict = get_card(game_deck_list)
        next_card_rank = next_card_dict['rank']
        next_card_suit = next_card_dict['suit']
        next_card_value = next_card_dict['value']
        print("Next card is: " + next_card_rank + " of " + next_card_suit)

    if answer == 'h': 
        if next_card_value > current_card_value:
            print("You got it right!!, card was higher")
            score = score + 20 
        else:
            print("sorry, card was not higher")
            score = score - 15

    elif answer == "l":
        if next_card_value > current_card_value:
            score = score + 20
            print("You got it right!!, card was lower")
        else:
            score = score - 15
            print("sorry, card was not lower")

    print(f"Your score is: {score}")
    print()
    current_card_rank = next_card_rank
    current_card_value = next_card_value # don't need current suit

    go_again = input("to play again, press ENTER, or 'q' to quit: ")
    if go_again == 'q':
        break

    print("OK see you soon!")    
