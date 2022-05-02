# polyomino

## Входные данные
На вход программы подаются 
```
T = (w,h) - размеры поля
R = [((w_r_i,h_r_i),n_r_i),...] - список прямоугольников
L = [((w_l_i,h_l_i),n_l_i),...] - список L-полиномино
```
Прямоуголькики имеют две ориентации: исходная и поворот на 90 градусов
L-полиномино имеют четыре ориентации: исходная и повороты на 90, 180, 270 градусов

Фигуры представляются как матрицы (w_i,h_i), состоящие из 0 и 1.

## Подготовка данных:
```
Каждую фигуру из списков R и L представляем во всех возможных ориентациях. 
Получаем список списков poly_list со всеми ориентациями каждой фигуры.

Для каждой фигуры poly из списка poly_list:
    Создаем matr - матрицу положений в простанстве фигуры poly, размерность (0,w*h)
    Для каждой ориентации p фигуры poly:
        Дополняем матрицу положения (w_i,h_i) нулями до размера поля (w,h) и вытягиваем [матрицу фигуры] в строку.
        Полученную строку добавляем в matr.
    Добавляем matr в список матриц положений фигур poly_matr_list.
```

## Решающий алгоритм `solve`: 
```
Вход:
    base_row        -   строка для сравнения
    poly_matr_list  -   список матриц положений фигур
    k               -   номер фигуры
    solutions=[]    -   список положений, добавленных в решение
Алгоритм:
    Выбираем k-тую матрицу положений фигуры poly из poly_matr_list
    Для каждой строки row из матрицы poly:
        Вычисляем сумму sum_row = base_row + sum_row
        Если sum_row не содержит чисел больших 1:
            добавить row в solutions
            Если длина poly_matr_list == k+1:
                вернуть True
            flag = solve(sum_row,poly_matr_list,k+1,solutions)
            Если flag == True:
                вернуть True
            исключить row из solutions
    вернуть False
```


## Пример работы программы
Входные данные в файле `input_data.json`
```
{
    "T": [3,5],
    "R": [
        [[2,2],1]
    ],
    "L": [
        [[3,2],1],
        [[2,2],2]
    ]
}
```
Результат выполнения
```
> python polyno.py
Найдено решение:
[[1. 1. 0.]
 [1. 1. 4.]
 [2. 4. 4.]
 [2. 3. 3.]
 [2. 2. 3.]]
```

