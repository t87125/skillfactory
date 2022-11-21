# skillfactory
Итоговое задание "Крестики-нолики" в модуле B5.6
# Название игры
print("=" * 10, " Игра Крестики-нолики для двух игроков ", "=" * 10)

# Создаём список для поля
board = list(range(1,10))

#Внутри программы игровое поле представлено в виде одномерного списка с числами от 1 до 9.
def create_board(board):
   print("-" * 13)
   for i in range(3):
      print("|", board[0+i*3], "|", board[1+i*3], "|", board[2+i*3], "|")
      print("-" * 13)

# Задачи блока:
# 1. Принять ввод пользователя.
# 2. Обработать некорректный ввод, например, введено не число. Для преобразования строки в число используем функцию int().
# 3. Обработать ситуации. когда клетка занята или когда введено число не из диапазона 1..9.
def user_input(user_selection):
   valid = False
   while not valid:
      user_answer = input("Куда поставим " + user_selection+"? ")
      try:
         user_answer = int(user_answer)
      except:
         print("Некорректный ввод. Необходимо проверить правильность ввода")
         continue
      if user_answer >= 1 and user_answer <= 9:
         if(str(board[user_answer-1]) not in "XO"):
            board[user_answer-1] = user_selection
            valid = True
         else:
            print("Клетка уже занята!")
      else:
        print("Некорректный ввод. Введите число от 1 до 9.")

#Посредством данного блока проверяется игровое поле.
# Создаём кортеж с выигрышными координатами и проходимся циклом for по нему.
# Если символы во всех трех заданных клетках равны – возвращаем выигрышный символ, иначе – возвращаем значение False.
# Непустая строка(выигрышный символ) при приведении ее к логическому типу вернет True.
def check_win(board):
   win_comb = ((0,1,2), (3,4,5), (6,7,8), (0,3,6), (1,4,7), (2,5,8), (0,4,8), (2,4,6))
   for each in win_comb:
       if board[each[0]] == board[each[1]] == board[each[2]]:
          return board[each[0]]
   return False

#В данном блоке создаем цикл while. Цикл выполняется пока один из игроков не выиграл. В данном цикле выводим игровое
#поле, принимаем ввод пользователя, определяя его выбор (x или о).

# Ждем, когда переменная counter станет больше 4 для того, чтобы избежать избыточного вызова функции check_win.
# Переменная tmp  создана для того, чтобы лишний раз не вызывать функцию check_win. “Запоминаем” ее значение и при
# необходимости используем в строке “print(tmp, “выиграл!”)”.
def main(board):
    counter = 0
    win = False
    while not win:
        create_board(board)
        if counter % 2 == 0:
           user_input("X")
        else:
           user_input("O")
        counter += 1
        if counter > 4:
           tmp = check_win(board)
           if tmp:
              print(tmp, "выиграл!")
              win = True
              break
        if counter == 9:
            print("У Вас ничья!")
            break
    create_board(board)
main(board)
