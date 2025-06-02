board = [' ' for _ in range(9)]

def print_board():
    print()
    for i in range(3):
        print(" " + board[3*i] + " | " + board[3*i+1] + " | " + board[3*i+2])
        if i < 2:
            print("---|---|---")
    print()

def check_winner(player):
    win_combos = [
        [0, 1, 2], [3, 4, 5], [6, 7, 8],
        [0, 3, 6], [1, 4, 7], [2, 5, 8],
        [0, 4, 8], [2, 4, 6]
    ]
    for combo in win_combos:
        if board[combo[0]] == board[combo[1]] == board[combo[2]] == player:
            return True
    return False

def is_draw():
    return ' ' not in board

def play_game():
    current_player = 'X'
    while True:
        print_board()
        try:
            move = int(input(f"Player {current_player}, enter your move (1-9): ")) - 1
            if move < 0 or move > 8 or board[move] != ' ':
                print("Invalid move. Try again.")
                continue
        except ValueError:
            print("Please enter a valid number.")
            continue

        board[move] = current_player

        if check_winner(current_player):
            print_board()
            print(f"Player {current_player} wins!")
            break

        if is_draw():
            print_board()
            print("It's a draw!")
            break

        current_player = 'O' if current_player == 'X' else 'X'

if _name_ == "_main_":
    play_game()