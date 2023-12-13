import random

def print_board(board):
    for row in board:
        print(" | ".join(row))
        print("-" * 5)

def check_winner(board, player):
    for i in range(3):
        if all(board[i][j] == player for j in range(3)) or all(board[j][i] == player for j in range(3)):
            return True
    if all(board[i][i] == player for i in range(3)) or all(board[i][2 - i] == player for i in range(3)):
        return True
    return False

def is_board_full(board):
    return all(board[i][j] != ' ' for i in range(3) for j in range(3))

def get_empty_cells(board):
    return [(i, j) for i in range(3) for j in range(3) if board[i][j] == ' ']

def player_move(board):
    while True:
        try:
            row = int(input("Enter the row (0, 1, or 2): "))
            col = int(input("Enter the column (0, 1, or 2): "))
            if board[row][col] == ' ':
                return row, col
            else:
                print("Cell already occupied. Try again.")
        except (ValueError, IndexError):
            print("Invalid input. Please enter a number between 0 and 2.")

def ai_move(board):
    empty_cells = get_empty_cells(board)
    return random.choice(empty_cells)

def play_tic_tac_toe():
    board = [[' ' for _ in range(3)] for _ in range(3)]
    players = ['X', 'O']
    turn = 0

    print("Welcome to Tic-Tac-Toe!")

    while True:
        print_board(board)
        current_player = players[turn % 2]

        if current_player == 'X':
            row, col = player_move(board)
        else:
            print("AI's turn:")
            row, col = ai_move(board)

        board[row][col] = current_player

        if check_winner(board, current_player):
            print_board(board)
            print(f"{current_player} wins!")
            break
        elif is_board_full(board):
            print_board(board)
            print("It's a draw!")
            break

        turn += 1

if __name__ == "__main__":
    play_tic_tac_toe()
