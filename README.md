# home_work
def print_board(board):
    """
    Функция для отображения текущего состояния игрового поля
    """
    print("\n   0   1   2")
    for i in range(3):
        print(f"{i}  {board[i][0]} | {board[i][1]} | {board[i][2]}")
        if i < 2:
            print("  -----------")


def check_winner(board):
    """
    Функция проверки завершенности игры
    Возвращает:
    - 'X' если победили крестики
    - 'O' если победили нолики
    - 'draw' если ничья
    - None если игра продолжается
    """
    # Проверка строк
    for row in board:
        if row[0] == row[1] == row[2] != ' ':
            return row[0]

    # Проверка столбцов
for col in range(3):
        if board[0][col] == board[1][col] == board[2][col] != ' ':
            return board[0][col]

    # Проверка диагоналей
if board[0][0] == board[1][1] == board[2][2] != ' ':
        return board[0][0]
    if board[0][2] == board[1][1] == board[2][0] != ' ':
        return board[0][2]

    # Проверка на ничью
if all(board[i][j] != ' ' for i in range(3) for j in range(3)):
        return 'draw'

return None


def is_valid_move(board, row, col):
    """
    Проверка корректности хода
    """
    if row not in [0, 1, 2] or col not in [0, 1, 2]:
        return False
    if board[row][col] != ' ':
        return False
    return True


def get_player_move(board, player):
    """
    Получение хода от игрока с проверкой корректности
    """
    while True:
        try:
            move = input(f"Игрок {player}, введите ваш ход (строка столбец, например '0 1'): ")
            row, col = map(int, move.split())

if is_valid_move(board, row, col):
                return row, col
            else:
                print("Некорректный ход! Попробуйте еще раз.")
        except (ValueError, IndexError):
            print("Ошибка ввода! Введите два числа через пробел (например: '0 1').")


def play_game():
    """
    Основная функция игры
    """
    # Инициализация игрового поля
    board = [[' ' for _ in range(3)] for _ in range(3)]
    current_player = 'X'

print("Добро пожаловать в игру Крестики-нолики!")
    print("Для хода введите номер строки и столбца через пробел (например: '0 1')")

while True:
        # Отображение текущего состояния поля
        print_board(board)

        # Получение хода от текущего игрока
        row, col = get_player_move(board, current_player)

        # Выполнение хода
        board[row][col] = current_player

        # Проверка состояния игры
        result = check_winner(board)

if result:
            print_board(board)
            if result == 'draw':
                print("Ничья! Игра завершена.")
            else:
                print(f"Победил игрок {result}! Поздравляем!")
            break

        # Смена игрока
current_player = 'O' if current_player == 'X' else 'X'


def main():
    """
    Главная функция с пользовательским интерфейсом
    """
    while True:
        play_game()

        # Предложение сыграть еще раз
play_again = input("\nХотите сыграть еще раз? (да/нет): ").lower()
        if play_again not in ['да', 'д', 'yes', 'y']:
            print("Спасибо за игру! До свидания!")
            break


# Запуск игры
if __name__ == "__main__":
    main()
