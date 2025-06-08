# tic-tac-toe-project-for-Micro-IT
def print_board(board):
    print("\n")
    for i in range(3):
        print(" " + " | ".join(board[i]))
        if i < 2:
            print("---+---+---")
    print("\n")

def check_winner(board, player):
    # Winning combinations: rows, columns, diagonals
    win_positions = [
        [(0,0), (0,1), (0,2)],
        [(1,0), (1,1), (1,2)],
        [(2,0), (2,1), (2,2)],
        [(0,0), (1,0), (2,0)],
        [(0,1), (1,1), (2,1)],
        [(0,2), (1,2), (2,2)],
        [(0,0), (1,1), (2,2)],
        [(0,2), (1,1), (2,0)],
    ]
    return any(all(board[r][c] == player for r, c in combo) for combo in win_positions)

def is_draw(board):
    return all(cell in ['X', 'O'] for row in board for cell in row)

def get_position(move):
    positions = {
        1: (0, 0), 2: (0, 1), 3: (0, 2),
        4: (1, 0), 5: (1, 1), 6: (1, 2),
        7: (2, 0), 8: (2, 1), 9: (2, 2),
    }
    return positions.get(move, (-1, -1))

def tic_tac_toe():
    board = [[' ' for _ in range(3)] for _ in range(3)]
    current_player = 'X'

    print("Welcome to Tic-Tac-Toe!")
    print("Box numbers:")
    print(" 1 | 2 | 3\n-----------\n 4 | 5 | 6\n-----------\n 7 | 8 | 9")
    print_board(board)

    while True:
        try:
            move = int(input(f"Player {current_player}, choose a box (1-9): "))
            if move not in range(1, 10):
                print("Invalid box. Choose a number from 1 to 9.")
                continue

            row, col = get_position(move)
            if board[row][col] != ' ':
                print("That spot is already taken. Try again.")
                continue

            board[row][col] = current_player
            print_board(board)

            if check_winner(board, current_player):
                print(f"Player {current_player} wins!")
                break

            if is_draw(board):
                print("It's a draw!")
                break

            current_player = 'O' if current_player == 'X' else 'X'

        except ValueError:
            print("Invalid input. Please enter a number from 1 to 9.")

# Run the game
tic_tac_toe()
