# Exam_04_01. Биномиальные коэффициенты.

## Задание

**Уровень:** 3  
**Темы:** Базовые управляющие структуры (следование, ветвление, повторение).  
**Директория для решения:** src/  
**Файлы решения:** main.c  
**Входные данные:** стандартный поток ввода (stdin)  
**Выходные данные:** стандартный поток вывода (stdout)  

Написать программу, осуществляющую вывод на стандартный поток stdout строки состоящей из биномиальных коэффициентов для `k=0..n` разделенных пробелами. `!` - операция взятия факториала, факториал числа n вычисляется как `n! = 1*2*3*...*n`, параметр n задается в виде неотрицательного целого числа через стандартный поток ввода stdin. В конце ответа не должно быть переноса на новую строку.

**Примечание:** за последним выведенным коэффициентом не должно следовать пробела.

## Примеры

| Входные данные | Результат работы |  
| 0 | 1 |  
| 1 | 1 1 |  
| 2 | 1 2 1 |  
| 3 | 1 3 3 1 |  

**Внимание:** Мы любезно напоминаем вам, что процедура тестирования вашей программы включает анализ стиля кода. Пожалуйста, загляните в папку materials/. Также обязательно проверяйте вашу программу на утечки памяти!
```c
#include <stdio.h>

unsigned long long factorial(int n) {
    unsigned long long result = 1;
    for (int i = 1; i <= n; ++i) {
        result *= i;
    }
    return result;
}

unsigned long long binomial_coefficient(int n, int k) {
    return factorial(n) / (factorial(k) * factorial(n - k));
}

int main(void) {
    int n;
    if (scanf("%d", &n) != 1 || n < 0) {
        printf("n/a");
        return 0;
    }

    for (int k = 0; k <= n; ++k) {
        if (k > 0) {
            printf(" ");
        }
        printf("%llu", binomial_coefficient(n, k));
    }

    return 0;
}
```
________________________________

# Exam_04_02. Поиск наибольшего.

## Задание

**Уровень:** 2  
**Темы:** Базовые управляющие структуры (следование, ветвление, повторение).  
**Директория для решения:** src/  
**Файлы решения:** main.c  
**Входные данные:** стандартный поток ввода (stdin)  
**Выходные данные:** стандартный поток вывода (stdout)  

Написать программу, осуществляющую поиск наибольшего числа в последовательности, состоящей из неотрицательных целых чисел. Последовательность задается на стандартный поток ввода stdin, элементы последовательности разделены между собой пробелами, концом последовательности, является число -1, которое обозначает конец последовательности и не является ее злементом. Найденное наибольшее значение необходимо вывести на стандартный поток вывода. Гарантируется, что в последоватальности всегда есть хоть один элемент. В конце ответа не должно быть переноса ка новую строку.

## Примеры

| Входные данные | Результат работы |  
| 1000 -1 | 1000 |  
| 1 2 3 4 3 2 1 -1 | 4 |  

**Внимание:** Мы любезно напоминаем вам, что процедура тестирования вашей программы включает анализ стиля кода. Пожалуйста, загляните в папку materials/. Также обязательно проверяйте вашу программу на утечки памяти!
```c
#include <stdio.h>

int main(void) {
    int num;
    int max = -1;

    while (scanf("%d", &num) == 1) {
        if (num == -1) {
            break;
        }
        if (num > max) {
            max = num;
        }
    }

    if (max == -1) {
        printf("n/a");
    } else {
        printf("%d", max);
    }

    return 0;
}
```
________________________________

# Exam_04_04. Наибольшая цифра.

## Задание

**Уровень:** 3  
**Темы:** Базовые управляющие структуры (следование, ветвление, повторение).  
**Директория для решения:** src/  
**Файлы решения:** main.c  
**Входные данные:** стандартный поток ввода (stdin)  
**Выходные данные:** стандартный поток вывода (stdout)  

Написать программу, осуществляющую вывод на стандартный поток stdout наибольшей цифры целого числа, которое задается на стандартном потоке ввода stdin. В конце ответа не должно быть переноса на новую строку. Проверить на валидность введенные данные. В случае любой ошибки выводить "n/a".

## Примеры

| Входные данные | Результат работы |  
| 123 | 3 |  
| 10 | 1 |  
| 111111 | 1 |  
| 0 | 0 |  

**Внимание:** Мы любезно напоминаем вам, что процедура тестирования вашей программы включает анализ стиля кода. Пожалуйста, загляните в папку materials/. Также обязательно проверяйте вашу программу на утечки памяти!
```c
#include <stdio.h>

int main(void) {
    char input[100];
    if (scanf("%s", input) != 1) {
        printf("n/a");
        return 0;
    }

    int max_digit = -1;
    for (int i = 0; input[i] != '\0'; ++i) {
        if (input[i] >= '0' && input[i] <= '9') {
            int digit = input[i] - '0';
            if (digit > max_digit) {
                max_digit = digit;
            }
        } else if (input[i] == '-' && i == 0) {
            continue;
        } else {
            printf("n/a");
            return 0;
        }
    }

    if (max_digit == -1) {
        printf("n/a");
    } else {
        printf("%d", max_digit);
    }

    return 0;
}
```
________________________________

# Exam_04_05. Произведение нечетных чисел.

## Задание

**Уровень:** 3  
**Темы:** Базовые управляющие структуры (следование, ветвление, повторение).  
**Директория для решения:** src/  
**Файлы решения:** main.c  
**Входные данные:** стандартный поток ввода (stdin)  
**Выходные данные:** стандартный поток вывода (stdout)  

Написать программу, осуществляющую вывод на стандартный поток stdout произведение нечетных цифр целого числа, подаваемого через стандартный поток ввода stdin. Если нечетных цифр в числе нет, вывести в качестве результата 0. В конце ответа не должно быть переноса на новую строку. Проверить на валидность введенные данные. В случае любой ошибки выводить "n/a".

## Примеры

| Входные данные | Результат работы |  
| 1234 | 3 |  
| 24 | 0 |  
| -3 | 3 |  

**Внимание:** Мы любезно напоминаем вам, что процедура тестирования вашей программы включает анализ стиля кода. Пожалуйста, загляните в папку materials/. Также обязательно проверяйте вашу программу на утечки памяти!
```c
#include <stdio.h>

int main(void) {
    char input[100];
    if (scanf("%s", input) != 1) {
        printf("n/a");
        return 0;
    }

    int product = 1;
    int has_odd = 0;

    for (int i = 0; input[i] != '\0'; ++i) {
        if (input[i] >= '0' && input[i] <= '9') {
            int digit = input[i] - '0';
            if (digit % 2 != 0) {
                product *= digit;
                has_odd = 1;
            }
        } else if (input[i] == '-' && i == 0) {
            continue;
        } else {
            printf("n/a");
            return 0;
        }
    }

    if (has_odd) {
        printf("%d", product);
    } else {
        printf("0");
    }

    return 0;
}
```
