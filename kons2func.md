# Функции
- именованный блок кода, который выполняет определённую задачу и может быть вызван из других частей программы/блок кода выполняющий определенную задачу
- создание функций
```py
def name()                   #create function
def sum(a, b):
    return a+b               #function with returning sum

def words(string):         #ввод функции
    symbols = []           #создание списка
    for i in range(len(string)):  
        if i % 2 == 0:            #проверка на четность
            symbols.append(string[i])
    return symbols
string = input()
symbols = words(string)
print(symbols)
```