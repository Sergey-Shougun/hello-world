b = list(range(1, 10)) #генерация списка с числами от одного до девяти

def d(x): #функция, создающая игровое поле
    print("-" * 13)
    for i in range(3):
        print("|", x[0 + i * 3], "|", x[1 + i * 3], "|", x[2 + i * 3], "|") # функция расчертит игровое поле с номерами
        print("-" * 13) #Номера нужны для удобства игры, также присутствуют поля для разграничения цифр


def t(x):
    win = False
    while not win: # цикл while не закончится, пока win не примет значение True
        ans = input("Выберите, куда поставить " + x) #функция требует число для ввода
        try:
            ans = int(ans) #программа пробует перевести число из строчного типа в целочисленный
        except ValueError: #если не получается перевести и программа ошибку выведет, функция перезапустится
            print("Вы ввели не число. Попробуйте ещё раз.")
            continue
        if 1 <= ans <= 9:#проверка на то, чтобы ответ находился в числовом диапозоне
            if str(b[ans - 1]) not in "XO":#если ячейка не занята, то туда будет поставлен символ
                b[ans - 1] = x
                win = True # заканчивается цикл и вместе с этим ход игрока, при этом не возникает никаких ошибок
            else: #если число выпадает на занятую ячейку, то сообщаем об этом игроку и его ход продолжается
                print("Эта ячейка уже занята. Попробуйте выбрать другую.")
        else: #если же число не входит в указанный выше диапозон, то также продолжается ход игрока
            print("Вы указали число, не входящее в диапозон от 1 до 9. Введите цифру, которая ещё есть на поле.")


def c(x): #функция для вычисления победы игрока. Указывается все победные комбинации.
    win = ((0, 1, 2), (3, 4, 5), (6, 7, 8), (0, 3, 6), (1, 4, 7), (2, 5, 8), (0, 4, 8), (2, 4, 6))
    for some in win:# Если есть хоть одно совпадение с указанными комбинациями, то функция возвращает символ победителя
        if x[some[0]] == x[some[1]] == x[some[2]]:
            return x[some[0]]
    return False #В противном случае возвращается False


def final(x): #Функция, которая непосредственно отвечает за игровой процесс
    count = 0 # Счётчик ходов
    win = False # Станет True как только будут выполнены условия победы кем-либо из игроков
    while not win:
        d(x) #Запускается функция для создания игрового поля.
        if count % 2 == 0: # Проверка счётчика ходов для очерёдности хода
            t("X")
        else:
            t("O")
        count += 1 # Включение слудеющего хода

        end = c(x)#В end передаётся значение функции, проверяющей победу кого-либо из
        if end: # Если функция c возвращает символ игрока, то функция пишет, кто выиграл и прекращает действие функции
            print(end, "выиграл!")
            win = True #win становится True и прекращает действие цикла
            break
        if count == 9: # Если счётчик ходов стал равен девяти, а функция c не выдала победителя, означает ничью
            print("Ничья!")
            break
    d(x) # Пишем конечный вариант поля


final(b) #Запускаем непосредственно программу
