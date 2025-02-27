# python-project
import random


def roll_dice():
    return random.randint(1, 6)


def initialize_board():
    
    ladders = {2: 38, 7: 14, 8: 31, 15: 26, 21: 42, 28: 84, 36: 44, 51: 67, 71: 91, 78: 98}
    snakes = {16: 6, 47: 26, 49: 11, 56: 53, 62: 19, 64: 60, 87: 24, 93: 73, 95: 75, 98: 78}
    
    board = {}
    board.update(ladders)
    board.update(snakes)
    return board


def play_game():
    board = initialize_board()
    
    
    player1_position = 1
    player2_position = 1
    
    current_player = 1  # Player 1 starts first
    
    while True:
        print(f"\nPlayer {current_player}'s turn:")
        input("Press Enter to roll the dice.")
        
        dice_roll = roll_dice()
        print(f"Player {current_player} rolled a {dice_roll}.")
        
        
        if current_player == 1:
            player1_position += dice_roll
            if player1_position > 100:
                player1_position = 100
            print(f"Player 1 moves to position {player1_position}.")
        else:
            player2_position += dice_roll
            if player2_position > 100:
                player2_position = 100
            print(f"Player 2 moves to position {player2_position}.")
        
        
        if current_player == 1 and player1_position in board:
            player1_position = board[player1_position]
            print(f"Player 1 landed on a special square and moved to position {player1_position}.")
        elif current_player == 2 and player2_position in board:
            player2_position = board[player2_position]
            print(f"Player 2 landed on a special square and moved to position {player2_position}.")
        
       
        if player1_position == 100:
            print("\nPlayer 1 wins!")
            break
        elif player2_position == 100:
            print("\nPlayer 2 wins!")
            break
        
        
        current_player = 2 if current_player == 1 else 1


play_game()
