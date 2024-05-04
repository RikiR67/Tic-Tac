# Tic-Tac
# Создаем пустое игровое поле
board = [' ' for _ in range(9)]

def print_board():
    print('-------------')
    for i in range(3):
        row = '| ' + ' | '.join(board[i*3:i*3+3]) + ' |'
        print(row)
        print('-------------')

def check_winner(board, player):
    # Проверяем все возможные комбинации для победы
    win_combinations = [[0,1,2], [3,4,5], [6,7,8],
                        [0,3,6], [1,4,7], [2,5,8],
                        [0,4,8], [2,4,6]]
    for combo in win_combinations:
        if all(board[i] == player for i in combo):
            return True
    return False

def is_board_full(board):
    return ' ' not in board

current_player = 'X'

while True:
    print_board()
    move = int(input(f'Игрок {current_player}, введите номер клетки (от 1 до 9): '))
    if board[move-1] == ' ':
        board[move-1] = current_player

        if check_winner(board, current_player):
            print_board()
            print(f'Игрок {current_player} выиграл!')
            break
        elif is_board_full(board):
            print_board()
            print('Ничья!')
            break
        else:
            current_player = 'O' if current_player == 'X' else 'X'
    else:
        print('Клетка занята, попробуйте другую.')
