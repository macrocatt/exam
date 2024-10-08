# Exam_05_01. Скалярное произведение.

## Задание

**Уровень:** 3  
**Темы:** динамические массивы  
**Директория для решения:** src/  
**Файлы решения:** main.c  
**Входные данные:** стандартный поток ввода (stdin)  
**Выходные данные:** стандартный поток вывода (stdout)  

Написать программу, производящую скалярное умножение двух векторов n-мерного пространства. Через входной поток ввода stdin задается целое положительное число n, обозначающее размерность пространства, затем следуют 2 строки: n целочисленных координат первого вектора и n целочисленных координат второго, разделенные пробелом. Результат вычислений вывести на стандартный поток вывода stdout. В конце ответа не должно быть переноса на новую строку. Проверить на валидность введенные данные. В случае любой ошибки выводить "n/a".

**Примечание:** последовательность может быть любого размера.

## Примеры

| Входные данные | Результат работы |  
| 1<br>7<br>3 | 21 |  
| 3<br>1 2 3<br>1 2 3 | 14 |  

**Внимание:** Мы любезно напоминаем вам, что процедура тестирования вашей программы включает анализ стиля кода. Пожалуйста, загляните в папку materials/. Также обязательно проверяйте вашу программу на утечки памяти!
```c
#include <stdio.h>
#include <stdlib.h>

int main() {
    int n;

    if (scanf("%d", &n) != 1 || n <= 0) {
        printf("n/a");
        return 0;
    }

    int *vector1 = (int *)malloc(n * sizeof(int));
    int *vector2 = (int *)malloc(n * sizeof(int));

    if(vector1 == NULL || vector2 == NULL) {
        printf("n/a");
        free(vector1);
        free(vector2);
        return 0;
    }

    for (int i = 0; i < n; i++){
        if (scanf("%d", &vector1[i]) != 1) {
            printf("n/a");
            free(vector1);
            free(vector2);
            return 0;
        }
    }

    for (int i = 0; i < n; i++){
        if (scanf("%d", &vector2[i]) != 1) {
            printf("n/a");
            free(vector1);
            free(vector2);
            return 0;
        }
    }
    int dot_product = 0;
    for (int i = 0; i < n; i++) {
        dot_product += vector1[i] * vector2[i];
    }

    printf("%d", dot_product);

    free(vector1);
    free(vector2);
    return 0;
}
```
________________________________

# Exam_05_03. Вывод последовательности.

## Задание

**Уровень:** 3  
**Темы:** динамические массивы  
**Директория для решения:** src/  
**Файлы решения:** main.c  
**Входные данные:** стандартный поток ввода (stdin)  
**Выходные данные:** стандартный поток вывода (stdout)  

Написать программу, производящую вывод элементов последовательности `x = (x_1, x_2, x_3, ..., x_n)` в следующем порядке `x_1 x_n x_2 x_{n-1}...`. Последовательность `x` состоит из целых неотрицательных чисел и задается на стандартном потоке ввода stdin, элементы последовательности разделены между собой пробелами, концом последовательности является число -1, которое обозначает конец последовательности и не является ее злементом. В конце ответа не должно быть переноса на новую строку. Проверить на валидность введенные данные. В случае любой ошибки выводить "n/a".

**Примечание:** за последним выведенным элементом не должно следовать пробела.

**Примечание:** последовательность может быть любого размера.

## Примеры

| Входные данные | Результат работы |  
| 1 2 3 -1 | 1 3 2 |  
| 1 2 3 4 5 6 -1 | 1 6 2 5 3 4 |  
| -1 |  |  

**Внимание:** Мы любезно напоминаем вам, что процедура тестирования вашей программы включает анализ стиля кода. Пожалуйста, загляните в папку materials/. Также обязательно проверяйте вашу программу на утечки памяти!
```c
#include <stdio.h>
#include <stdlib.h>

int main() {
    int num, count = 0;
    int *sequence = NULL;

    // Чтение последовательности до -1
    while (scanf("%d", &num) == 1 && num != -1) {
        int *temp = realloc(sequence, (count + 1) * sizeof(int));
        if (temp == NULL) {
            free(sequence);
            printf("n/a");
            return 0;
        }
        sequence = temp;
        sequence[count++] = num;
    }

    // Проверка корректности завершения ввода
    if (num != -1) {
        free(sequence);
        printf("n/a");
        return 0;
    }

    // Вывод элементов в требуемом порядке
    for (int i = 0; i < count / 2; i++) {
        if (i > 0) {
            printf(" ");
        }
        printf("%d %d", sequence[i], sequence[count - 1 - i]);
    }

    // Если количество элементов нечетное, выведем средний элемент
    if (count % 2 != 0) {
        if (count > 1) {
            printf(" ");
        }
        printf("%d", sequence[count / 2]);
    }

    free(sequence);

    return 0;
}
```
________________________________

# Exam_05_04. Removing repetitions.

## Задание

**Уровень:** 3  
**Темы:** динамические массивы  
**Директория для решения:** src/  
**Файлы решения:** main.c  
**Входные данные:** стандартный поток ввода (stdin)  
**Выходные данные:** стандартный поток вывода (stdout)  

Написать программу, производящую удаление повторяющихся элементов последовательности, состоящей из целых неотрицательных чисел. Последовательность задается на стандартном потоке ввода stdin, элементы последовательности разделены между собой пробелами, концом последовательности является число -1, которое обозначает конец последовательности и не является ее злементом. Вывести элементы результирующей последовательности, разделенные между собой пробелами, на стандартный поток вывода stdout. В конце ответа не должно быть переноса на новую строку. Проверить на валидность введенные данные. В случае любой ошибки выводить "n/a".

**Примечание:** Порядок вывода элементов в результирующей последовательности определяется порядком первых вхождений соответствующих значений в первоначальной последовательности.

**Примечание:** последовательность может быть любого размера.

## Примеры

| Входные данные | Результат работы |  
| 1 1 2 2 3 -1 | 1 2 3 |  
| 1 2 1 3 1 4 -1 | 1 2 3 4 |  
| -1 |  |  

**Внимание:** Мы любезно напоминаем вам, что процедура тестирования вашей программы включает анализ стиля кода. Пожалуйста, загляните в папку materials/. Также обязательно проверяйте вашу программу на утечки памяти!
```c
#include <stdio.h>
#include <stdlib.h>

int main() {
    int num, count = 0;
    int *sequence = NULL;

    // Чтение последовательности до -1
    while (scanf("%d", &num) == 1 && num != -1) {
        int *temp = realloc(sequence, (count + 1) * sizeof(int));
        if (temp == NULL) {
            free(sequence);
            printf("n/a");
            return 0;
        }
        sequence = temp;
        sequence[count++] = num;
    }

    // Проверка корректности завершения ввода
    if (num != -1) {
        free(sequence);
        printf("n/a");
        return 0;
    }

    // Удаление повторов и сохранение порядка первых вхождений
    int *result = (int *)malloc(count * sizeof(int));
    if (result == NULL) {
        free(sequence);
        printf("n/a");
        return 0;
    }
    int result_count = 0;

    for (int i = 0; i < count; i++) {
        int duplicate = 0;
        for (int j = 0; j < result_count; j++) {
            if (sequence[i] == result[j]) {
                duplicate = 1;
                break;
            }
        }
        if (!duplicate) {
            result[result_count++] = sequence[i];
        }
    }

    // Вывод результирующей последовательности
    for (int i = 0; i < result_count; i++) {
        if (i > 0) {
            printf(" ");
        }
        printf("%d", result[i]);
    }

    free(sequence);
    free(result);

    return 0;
}
```
________________________________

# Exam_05_05. Реверс последовательности.

## Задание

**Уровень:** 2  
**Темы:** динамические массивы  
**Директория для решения:** src/  
**Файлы решения:** main.c  
**Входные данные:** стандартный поток ввода (stdin)  
**Выходные данные:** стандартный поток вывода (stdout)  

Написать программу, осуществляющую вывод на стандартный поток stdout через пробел в обратном порядке элементов последовательности, состоящей из целых неотрицательных чисел. Последовательность задается на стандартный поток ввода stdin, элементы последовательности разделены между собой пробелами, концом последовательности является число -1, которое обозначает конец последовательности и не является ее элементом. В конце ответа не должно быть переноса на новую строку. Проверить на валидность введенные данные. В случае любой ошибки выводить "n/a".

**Примечание:** последовательность может быть любого размера.

## Примеры

| Входные данные | Результат работы |  
| 1 2 3 4 5 -1 | 5 4 3 2 1 |  
| 1 1 1 2 2 2 -1 | 2 2 2 1 1 1 |  
| -1 |  |  

**Внимание:** Мы любезно напоминаем вам, что процедура тестирования вашей программы включает анализ стиля кода. Пожалуйста, загляните в папку materials/. Также обязательно проверяйте вашу программу на утечки памяти!
```c
#include <stdio.h>
#include <stdlib.h>

int main() {
    int num, count = 0;
    int *sequence = NULL;

    // Чтение последовательности до -1
    while (scanf("%d", &num) == 1 && num != -1) {
        int *temp = realloc(sequence, (count + 1) * sizeof(int));
        if (temp == NULL) {
            free(sequence);
            printf("n/a");
            return 0;
        }
        sequence = temp;
        sequence[count++] = num;
    }

    // Проверка корректности завершения ввода
    if (num != -1) {
        free(sequence);
        printf("n/a");
        return 0;
    }

    // Вывод элементов в обратном порядке
    for (int i = count - 1; i >= 0; i--) {
        if (i < count - 1) {
            printf(" ");
        }
        printf("%d", sequence[i]);
    }

    free(sequence);

    return 0;
}
```
