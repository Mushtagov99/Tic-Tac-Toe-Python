def draw_board(board):
    """Display the game board."""
    for i in range(0, len(board), 3):
        print(" " + " | ".join(str(cell) for cell in board[i:i+3]))
        if i < len(board) - 3:
            print("---|---|---")


def game_step(board, index, char):
    """Make a move on the game board."""
    if index < 1 or index > 9 or board[index - 1] in ('x', 'o'):
        return False
    board[index - 1] = char
    return True


def check_win(board):
    """Check for a win."""
    win_combinations = [
        (0, 1, 2), (3, 4, 5), (6, 7, 8),  # horizontal lines
        (0, 3, 6), (1, 4, 7), (2, 5, 8),  # vertical lines
        (0, 4, 8), (2, 4, 6)             # diagonal lines
    ]
    for pos in win_combinations:
        if board[pos[0]] == board[pos[1]] == board[pos[2]]:
            return board[pos[0]]
    return False


def start_game():
    """Start the game."""
    board = [1, 2, 3, 4, 5, 6, 7, 8, 9]
    current_player = 'x'
    step = 1
    draw_board(board)

    while step < 10 and not check_win(board):
        index = input(f'Turn player {current_player}. Enter a number (1-9) to place your mark (0 to exit): ')

        if index == '0':
            break

        index = int(index)
        if game_step(board, index, current_player):
            print('Successful move!')
            current_player = 'o' if current_player == 'x' else 'x'
            draw_board(board)
            step += 1
        else:
            print('Invalid input! Try again.')

    if step == 10:
        print('It\'s a draw!')
    else:
        print(f'Player {check_win(board)} wins!')


print('Welcome to Tic-Tac-Toe')
start_game()
