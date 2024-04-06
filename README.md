Цели и задачи работы: изучение функций ввода-вывода данных, про-граммирования вычисления значения выражения.
Задание к работе: 
1. Реализовать линейный вычислительный процесс. Самостоятельно ре-шить задачу в соответствии с индивидуальным вариантом. Реализовать представленные задачи на языках программирования JavaScript, Go (Golang), Swift, С, Haskell, Ruby, Rust, C++, Python, Java, Kotlin.
 2. Реализовать линейный вычислительный процесс любого задания на языке программирования Assembler. 
3. Представленные задачи можно реализовать на каждом языке в одной программе с последовательным выполнением. 
Методика выполнения работы:
1.Определить типы используемых в программе данных.
2.Описать переменные.
3.Написать функции ввода-вывода.
4.Разработать алгоритм решения задачи по индивидуальному заданию.
5.Написать и отладить программу с вводом-выводом информации
6.Протестировать работу программы на различных исходных данных.
7.Изменить формат вывода, проверить работу программы при другом формате вывода.
Задание 1.  Студенту не хочется выполнять лабораторную работу. Он должен начать выполнять ее немедленно, чтобы уложиться в срок. Задание - напечатать строку. За раз он может выполнить одну из следующих опе-раций: - добавить символ в конце строки; - добавить копию текущей стро-ки в конец (можно применить единожды). Помогите студенту найти мини-мальное количество операций, необходимых для ввода заданной строки. 
Пример: s=’’dbadbaa’ 
Результат: 5 = d->db->dba->dbadba->a. 
Задание 2. Дано целое число n— количество команд в турнире со стран-ными правилами: 
• Если текущее количество команд четное , каждая команда объединяется с другой командой. Всего n / 2сыграно матчей, и n / 2команды проходят в следующий раунд. 
• Если текущее количество команд нечетное , одна команда случайным об-разом продвигается в турнире, а остальные распределяются по парам. Всего (n - 1) / 2сыграно матчей, и (n - 1) / 2 + 1команды проходят в следу-ющий раунд. Возвращает количество матчей, сыгранных в турнире, пока не будет определен победитель.
Задание 3. Все числа из последовательности, которые составлены из цифр, идущих возрастанию необходимо перевернуть Пример. Вход: 4 87 129 33 45 Выход: 921 54.
Задание 1.
Python
def min_operations(input_string):
   Длина входной строки
  n = len(input_string)
   Массив для хранения минимального количества операций для каждого индекса
  dp = [0] * (n + 1)
   Словарь для хранения индекса последнего вхождения каждого символа
  last_occurrence = {}
   Проходим по каждому символу входной строки
  for i in range(1, n + 1):
     Инициализируем dp[i] как dp[i-1] + 1, предполагая, что необходимо добавить один символ
    dp[i] = dp[i-1] + 1
     Если текущий символ уже существует в словаре last_occurrence
    if input_string[i-1] in last_occurrence:
       Обновляем dp[i] как минимум между текущим dp[i] и dp последнего вхождения символа + 1
      dp[i] = min(dp[i], dp[last_occurrence[input_string[i-1]]] + 1)
     Обновляем словарь last_occurrence индексом текущего символа
    last_occurrence[input_string[i-1]] = i
   Возвращаем минимальное количество операций, необходимых для всей строки
  return dp[n]
 Получаем от пользователя строку
input_string = input()
 Вызываем функцию и выводим результат
print(min_operations(input_string))

 



Rust
use std::collections::HashMap;
use std::io;

// Функция для вычисления минимального количества операций
fn min_operations(input_string: &str) -> usize {
    // Длина входной строки
    let n = input_string.len();
    // Вектор для хранения минимального количества операций для каждого индекса
    let mut dp = vec![0; n + 1];
    // Хэш-карта для хранения последнего вхождения каждого символа
    let mut last_occurrence = HashMap::new();

    // Проходим по каждому символу входной строки
    for i in 1..=n {
        // Инициализируем dp[i] как dp[i-1] + 1, предполагая, что необходимо добавить один символ
        dp[i] = dp[i - 1] + 1;

        // Если последнее вхождение текущего символа существует в хэш-карте
        if let Some(&idx) = last_occurrence.get(&input_string.chars().nth(i - 1).unwrap()) {
            // Обновляем dp[i] как минимум между текущим dp[i] и dp послед-него вхождения символа + 1
            dp[i] = dp[i].min(dp[idx] + 1);
        }

        // Обновляем хэш-карту последнего вхождения текущего символа
        last_occurrence.insert(input_string.chars().nth(i - 1).unwrap(), i);
    }

    // Возвращаем минимальное количество операций для всей строки
    dp[n]
}

fn main() {
    // Выводим приглашение пользователю ввести строку
    println!("Введите строку:");
    // Создаем переменную для хранения введенной строки
    let mut input_string = String::new();
    // Читаем строку из стандартного ввода
    io::stdin().read_line(&mut input_string).expect("Не удалось прочитать строку");
    // Удаляем лишние пробелы и символы новой строки из введенной стро-ки
    let input_string = input_string.trim();

    // Вызываем функцию min_operations и выводим результат
    println!("Минимальное количество операций: {}", min_operations(input_string));
}

 

Ruby
def min_operations(input_string)
   Получаем длину входной строки
  n = input_string.length
   Создаем массив для хранения минимального количества операций для каждого индекса
  dp = Array.new(n + 1, 0)
   Создаем хэш-таблицу для хранения последнего вхождения каждого символа
  last_occurrence = {}	

   Проходим по каждому символу входной строки
  (1..n).each do |i|
     Инициализируем dp[i] как dp[i-1] + 1, предполагая, что необходимо добавить один символ
    dp[i] = dp[i - 1] + 1

     Если последнее вхождение текущего символа существует в хэш-таблице
    if last_occurrence.key?(input_string[i - 1])
       Обновляем dp[i] как минимум между текущим dp[i] и dp последнего вхождения символа + 1
      dp[i] = [dp[i], dp[last_occurrence[input_string[i - 1]]] + 1].min
    end

     Обновляем хэш-таблицу последнего вхождения текущего символа
    last_occurrence[input_string[i - 1]] = i
  end
  
   Возвращаем минимальное количество операций для всей строки
  return dp[n]
end

 Выводим приглашение пользователю ввести строку
print "Введите строку: "
 Получаем ввод пользователя и убираем лишние символы (перенос стро-ки)
input_string = gets.chomp
 Вызываем функцию и выводим результат
puts "Минимальное количество операций: {min_operations(input_string)}" 

Java
import java.util.HashMap;
import java.util.Scanner;

public class Main {
    // Метод для вычисления минимального количества операций
    public static int minOperations(String inputString) {
        // Получаем длину входной строки
        int n = inputString.length();
        // Создаем массив для хранения минимального количества операций для каждого индекса
        int[] dp = new int[n + 1];
        // Создаем хэш-таблицу для хранения последнего вхождения каждого символа
        HashMap<Character, Integer> lastOccurrence = new HashMap<>();

        // Проходим по каждому символу входной строки
        for (int i = 1; i <= n; i++) {
            // Инициализируем dp[i] как dp[i-1] + 1, предполагая, что необхо-димо добавить один символ
            dp[i] = dp[i - 1] + 1;

            // Получаем текущий символ
            char currentChar = inputString.charAt(i - 1);
            // Если последнее вхождение текущего символа существует в хэш-таблице
            if (lastOccurrence.containsKey(currentChar)) {
                // Обновляем dp[i] как минимум между текущим dp[i] и dp по-следнего вхождения символа + 1
                dp[i] = Math.min(dp[i], dp[lastOccurrence.get(currentChar)] + 1);
            }

            // Обновляем хэш-таблицу последнего вхождения текущего символа
            lastOccurrence.put(currentChar, i);
        }

        // Возвращаем минимальное количество операций для всей строки
        return dp[n];
    }

    public static void main(String[] args) {
        // Создаем объект Scanner для чтения ввода пользователя
        Scanner scanner = new Scanner(System.in);
        // Выводим приглашение для пользователя ввести строку
        System.out.print("Введите строку: ");
        // Считываем введенную строку
        String inputString = scanner.nextLine();
        // Выводим минимальное количество операций
        System.out.println("Минимальное количество операций: " + minOpera-tions(inputString));
        // Закрываем объект Scanner
        scanner.close();
    }
}

 

JavaScript
// Функция для вычисления минимального количества операций
function minOperations(inputString) {
    // Получаем длину входной строки
    const n = inputString.length;
    // Создаем массив для хранения минимального количества операций для каждого индекса
    const dp = new Array(n + 1).fill(0);
    // Создаем объект для хранения последнего вхождения каждого символа
    const lastOccurrence = {};

    // Проходим по каждому символу входной строки
    for (let i = 1; i <= n; i++) {
        // Инициализируем dp[i] как dp[i-1] + 1, предполагая, что необходимо добавить один символ
        dp[i] = dp[i - 1] + 1;

        // Если последнее вхождение текущего символа существует в объекте lastOccurrence
        if (lastOccurrence[inputString[i - 1]] !== undefined) {
            // Обновляем dp[i] как минимум между текущим dp[i] и dp послед-него вхождения символа + 1
            dp[i] = Math.min(dp[i], dp[lastOccurrence[inputString[i - 1]]] + 1);
        }

        // Обновляем объект lastOccurrence последним индексом текущего символа
        lastOccurrence[inputString[i - 1]] = i;
    }

    // Возвращаем минимальное количество операций для всей строки
    return dp[n];
}

// Создаем интерфейс для чтения ввода пользователя из стандартного по-тока ввода
const readline = require('readline');
const rl = readline.createInterface({
    input: process.stdin,
    output: process.stdout
});

// Задаем вопрос пользователю и ожидаем ввода
rl.question("", function(inputString) {
    // Вызываем функцию minOperations и выводим результат
    console.log(minOperations(inputString));
    // Закрываем интерфейс чтения
    rl.close();
});
 

C
using System;
using System.Collections.Generic;

class Program
{
    // Функция для определения минимального количества операций
    static int MinOperations(string inputString)
    {
        int n = inputString.Length;
        int[] dp = new int[n + 1]; // Массив для хранения результатов подзадач
        Dictionary<char, int> lastOccurrence = new Dictionary<char, int>(); // Словарь для отслеживания последнего вхождения каждого символа

        for (int i = 1; i <= n; i++)
        {
            dp[i] = dp[i - 1] + 1; // Инициализируем dp[i] значением dp[i-1] + 1

            // Если символ уже встречался ранее
            if (lastOccurrence.ContainsKey(inputString[i - 1]))
            {
                int idx = lastOccurrence[inputString[i - 1]]; // Получаем индекс последнего вхождения символа
                dp[i] = Math.Min(dp[i], dp[idx] + 1); // Обновляем dp[i] как минимум между текущим значением и dp[idx] + 1
            }

            lastOccurrence[inputString[i - 1]] = i; // Запоминаем индекс текущего вхождения символа
        }

        return dp[n]; // Возвращаем минимальное количество операций
    }

    static void Main(string[] args)
    {
        Console.Write("Введите строку: ");
        string inputString = Console.ReadLine();
        Console.WriteLine("Минимальное количество операций: " + MinOpera-tions(inputString));
    }
}
 


Swift
import Foundation

// Функция для вычисления минимального количества операций
func minOperations(_ inputString: String) -> Int {
    // Получаем длину входной строки
    let n = inputString.count
    // Создаем массив для хранения минимального количества операций для каждого индекса
    var dp = [Int](repeating: 0, count: n + 1)
    // Создаем словарь для хранения последнего вхождения каждого симво-ла
    var lastOccurrence = [Character: Int]()

    // Проходим по каждому символу входной строки
    for i in 1...n {
        // Инициализируем dp[i] как dp[i-1] + 1, предполагая, что необходимо добавить один символ
        dp[i] = dp[i - 1] + 1

        // Получаем текущий символ
        let currentChar = inputString[inputString.index(inputString.startIndex, offsetBy: i - 1)]
        // Если последнее вхождение текущего символа существует в словаре lastOccurrence
        if let index = lastOccurrence[currentChar] {
            // Обновляем dp[i] как минимум между текущим dp[i] и dp послед-него вхождения символа + 1
            dp[i] = min(dp[i], dp[index] + 1)
        }

        // Обновляем словарь lastOccurrence последним индексом текущего символа
        lastOccurrence[currentChar] = i
    }

    // Возвращаем минимальное количество операций для всей строки
    return dp[n]
}

// Печатаем приглашение для пользователя ввести строку
print("Введите строку: ", terminator: "")
// Считываем введенную строку
if let inputString = readLine() {
    // Вызываем функцию minOperations и выводим результат
    print("Минимальное количество операций: \(minOperations(inputString))")
}
 
C++
include <iostream>
include <string>
include <unordered_map>

// Функция для вычисления минимального количества операций
int minOperations(const std::string& inputString) {
    // Получаем длину входной строки
    int n = inputString.length();
    // Создаем массив dp для хранения минимального количества операций для каждого индекса
    int dp[n + 1];
    // Создаем хэш-таблицу lastOccurrence для хранения последнего вхож-дения каждого символа
    std::unordered_map<char, int> lastOccurrence;

    // Инициализируем dp[0] как 0
    dp[0] = 0;

    // Проходим по каждому символу входной строки
    for (int i = 1; i <= n; i++) {
        // Инициализируем dp[i] как dp[i-1] + 1, предполагая, что необходимо добавить один символ
        dp[i] = dp[i - 1] + 1;

        // Если текущий символ уже встречался ранее
        if (lastOccurrence.find(inputString[i - 1]) != lastOccurrence.end()) {
            // Обновляем dp[i] как минимум между текущим dp[i] и dp послед-него вхождения символа + 1
            dp[i] = std::min(dp[i], dp[lastOccurrence[inputString[i - 1]]] + 1);
        }

        // Обновляем хэш-таблицу lastOccurrence последним индексом теку-щего символа
        lastOccurrence[inputString[i - 1]] = i;
    }

    // Возвращаем минимальное количество операций для всей строки
    return dp[n];
}

int main() {
    std::string inputString;
    // Выводим приглашение для пользователя ввести строку
    std::cout << "Введите строку: ";
    // Считываем введенную строку
    std::getline(std::cin, inputString);
    // Вызываем функцию minOperations и выводим результат
    std::cout << "Минимальное количество операций: " << minOpera-tions(inputString) << std::endl;
    return 0;
}
 

Go
package main

import (
	"fmt"
)

// Функция minOperations принимает входную строку и возвращает мини-мальное количество операций
// для приведения строки к последовательности символов без повторений.
func minOperations(inputString string) int {
	n := len(inputString)          // Получаем длину входной строки
	dp := make([]int, n+1)         // Создаем массив для хранения результа-тов подзадач
	lastOccurrence := make(map[byte]int) // Создаем карту для хранения индексов последнего вхождения символов

	for i := 1; i <= n; i++ { // Итерируем по всем символам входной строки
		dp[i] = dp[i-1] + 1 // Инициализируем текущий результат как результат предыдущей операции + 1

		// Если символ уже встречался, обновляем текущий результат, используя индекс последнего вхождения символа
		if idx, ok := lastOccurrence[inputString[i-1]]; ok {
			dp[i] = min(dp[i], dp[idx]+1)
		}

		lastOccurrence[inputString[i-1]] = i // Обновляем индекс последнего вхождения символа
	}

	return dp[n] // Возвращаем результат для всей строки
}

// Функция min возвращает минимальное из двух чисел.
func min(a, b int) int {
	if a < b {
		return a
	}
	return b
}

func main() {
	var inputString string
	fmt.Print("Введите строку: ")
	fmt.Scanln(&inputString) // Запрашиваем строку у пользователя
	fmt.Println("Минимальное количество операций:", minOpera-tions(inputString)) // Выводим результат работы функции minOperations
}

 

Kotlin
fun minOperations(inputString: String): Int {
    val n = inputString.length
    val dp = IntArray(n + 1) { 0 } // Массив для хранения минимального ко-личества операций для каждого индекса
    val lastOccurrence = mutableMapOf<Char, Int>() // Хранит последнее вхождение символа

    for (i in 1..n) {
        dp[i] = dp[i - 1] + 1 // Инициализация значения dp[i] на основе преды-дущего значения

        // Если текущий символ встречался ранее
        if (inputString[i - 1] in lastOccurrence) {
            // Обновляем значение dp[i] с учетом минимального числа операций
            dp[i] = minOf(dp[i], dp[lastOccurrence[inputString[i - 1]]!!] + 1)
        }

        // Запоминаем индекс последнего вхождения текущего символа
        lastOccurrence[inputString[i - 1]] = i
    }

    return dp[n] // Возвращаем минимальное количество операций для всей строки
}

fun main() {
    // Читаем строку из ввода
    val inputString = readLine()!!
    // Вызываем функцию minOperations и выводим результат
    println("${minOperations(inputString)}")
}
 

Задание 2.
Python
def tournament_matches(n):
     Инициализируем переменную для подсчета матчей
    matches = 0
    	
     Пока количество команд больше 1
    while n > 1:
         Если количество команд четное
        if n % 2 == 0:
             Добавляем к количеству матчей половину числа команд
            matches += n // 2
             Делим количество команд на два
            n //= 2
        else:
             Если количество команд нечетное, добавляем к количеству матчей половину числа команд минус одна
            matches += (n - 1) // 2
             Вычисляем новое количество команд после игры половины ко-манд
            n = (n - 1) // 2 + 1
    
     Возвращаем общее количество матчей
    return matches

 Пример использования:
n = int(input("Введите количество команд в турнире: "))
print("Количество матчей в турнире:", tournament_matches(n))

 

Rust
use std::io;

fn count_matches(mut n: u32) -> u32 {
    let mut matches = 0;
    while n > 1 {
        if n % 2 == 0 {
            matches += n / 2;
            n /= 2;
        } else {
            matches += (n - 1) / 2;
            n = (n - 1) / 2 + 1;
        }
    }
    matches
}

fn main() {
    println!("Введите количество команд в турнире:");
    let mut input = String::new();
    io::stdin().read_line(&mut input).expect("Ошибка чтения строки");
    let n: u32 = input.trim().parse().expect("Введено некорректное число");

    println!("Количество матчей: {}", count_matches(n));
}

 

Ruby
def count_matches(n)
  matches = 0
   Пока число команд больше 1
  while n > 1
     Если число команд четное
    if n.even?
       Добавляем к числу матчей половину числа команд
      matches += n / 2
       Уменьшаем число команд вдвое
      n /= 2
    else
       Если число команд нечетное, добавляем к числу матчей половину числа команд минус одна
      matches += (n - 1) / 2
       Уменьшаем число команд на единицу, а затем делим его на два и прибавляем один, чтобы получить новое число команд
      n = (n - 1) / 2 + 1
    end
  end
   Возвращаем общее количество матчей
  return matches
end

 Пример использования:
puts "Введите количество команд:"
n = gets.chomp.to_i
puts "Количество сыгранных матчей: {count_matches(n)}"

 

Java
import java.util.Scanner;

public class TournamentMatches {
    
    // Метод для вычисления общего количества матчей в турнире
    public static int numberOfMatches(int n) {
        int matches = 0;
        
        // Пока количество команд больше 1
        while (n > 1) {
            // Если количество команд четное
            if (n % 2 == 0) {
                // Добавляем к количеству матчей половину числа команд
                matches += n / 2;
                // Делим количество команд на два
                n /= 2;
            } else {
                // Если количество команд нечетное, добавляем к количеству матчей половину числа команд минус одна
                matches += (n - 1) / 2;
                // Вычисляем новое количество команд после игры половины ко-манд
                n = (n - 1) / 2 + 1;
            }
        }
        
        // Возвращаем общее количество матчей
        return matches;
    }
    
    public static void main(String[] args) {
        // Создаем объект Scanner для чтения ввода пользователя
        Scanner scanner = new Scanner(System.in);
        // Выводим приглашение для пользователя ввести количество команд в турнире
        System.out.print("Введите количество команд в турнире: ");
        // Считываем количество команд
        int n = scanner.nextInt();
        // Закрываем объект Scanner
        scanner.close();
        
        // Выводим количество матчей в турнире
        System.out.println("Количество матчей в турнире: " + numberOfMatch-es(n));
    }
}

 

JavaScript
// Подключаем модуль readline для взаимодействия с пользователем через консоль
const readline = require('readline');

// Создаем интерфейс для чтения из стандартного потока ввода (input) и записи в стандартный поток вывода (output)
const rl = readline.createInterface({
  input: process.stdin,
  output: process.stdout
});

// Функция для вычисления общего количества матчей в турнире
function countMatches(n) {
    let matches = 0;
    // Пока количество команд больше 1
    while (n > 1) {
        // Добавляем к количеству матчей половину числа команд
        matches += Math.floor(n / 2);
        // Если количество команд четное, делим его на 2, иначе вычитаем 1, делим на 2 и добавляем 1
        n = (n % 2 === 0) ? n / 2 : (n - 1) / 2 + 1;
    }
    return matches;
}

// Задаем вопрос пользователю через интерфейс
rl.question("", (answer) => {
  // Преобразуем введенный ответ в число
  const n = parseInt(answer);
  // Проверяем, является ли введенное значение числом больше 0
  if (!isNaN(n) && n > 0) {
    // Если это так, вызываем функцию countMatches и выводим результат
    console.log(countMatches(n));
    // Закрываем интерфейс после завершения работы
    rl.close();
  } else {
    // Если введенное значение не является положительным числом, просто закрываем интерфейс
    rl.close();
  }
});
 
C
using System;

class Program
{
    // Функция для расчета количества матчей в турнире
    static int CalculateMatches(int n)
    {
        int matches = 0;
        while (n > 1)
        {
            if (n % 2 == 0)
            {
                matches += n / 2;
                n /= 2;
            }
            else
            {
                matches += (n - 1) / 2;
                n = (n - 1) / 2 + 1;
            }
        }
        return matches;
    }

    static void Main(string[] args)
    {
        Console.WriteLine("Введите количество команд в турнире:");
        int n = int.Parse(Console.ReadLine() ?? "0"); // Читаем количество ко-манд

        int totalMatches = CalculateMatches(n); // Рассчитываем количество матчей
        Console.WriteLine($"Количество матчей в турнире: {totalMatches}"); // Выводим результат
    }
}
 

Assembler
INCLUDE Irvine32.inc

.data
    matches DWORD ?
    n DWORD 7 ; Предопределенное значение количества команд

.code
tournament_matches PROC
    mov matches, 0
    
    while_loop:
        cmp n, 1
        jle end_while
        
        test n, 1
        jz even_case

        ; Нечетное
        mov eax, n
        dec eax
        shr eax, 1
        add matches, eax
        inc n
        jmp next_iteration

        even_case:
        ; Четное
        mov eax, n
        shr eax, 1
        add matches, eax

        next_iteration:
        shr n, 1
        jmp while_loop

    end_while:
    ret
tournament_matches ENDP

main PROC
    ; Вызов функции tournament_matches
    call tournament_matches

    ; Вывод результата
    mov eax, matches
    call WriteDec
    call Crlf

    ; Завершение программы
    call ExitProcess

main ENDP

END main
 

Swift
// Функция для вычисления общего количества матчей в турнире
func countMatches(_ n: Int) -> Int {
    var matches = 0
    var teams = n
    
    // Пока количество команд больше 1
    while teams > 1 {
        // Если количество команд четное
        if teams % 2 == 0 {
            // Добавляем к количеству матчей половину числа команд
            matches += teams / 2
            // Делим количество команд на два
            teams /= 2
        } else {
            // Если количество команд нечетное, добавляем к количеству матчей половину числа команд минус одна
            matches += (teams - 1) / 2
            // Вычисляем новое количество команд после игры половины ко-манд
            teams = (teams - 1) / 2 + 1
        }
    }
    
    // Возвращаем общее количество матчей
    return matches
}

// Выводим приглашение для пользователя ввести количество команд в турнире
print("Введите количество команд в турнире:")
// Считываем введенное пользователем значение
if let input = readLine(), let n = Int(input) {
    // Вызываем функцию countMatches и выводим результат
    print("Количество матчей: \(countMatches(n))")
}

 

C++
include <iostream>
using namespace std;

int main() 
{
    // Запрашиваем количество команд у пользователя
    int teamsAmount;
    cin >> teamsAmount;
    
    int winner = teamsAmount;
    int matches_played;
    int counter_matches = 0;
    // Пока есть победитель (1 команда)
    while(winner != 1){
        // Если количество команд четное
        if (teamsAmount % 2 == 0) {
            // Вычисляем количество сыгранных матчей (половина от общего количества команд)
            matches_played = teamsAmount / 2;
            // Обновляем количество победителей (половина от общего количе-ства команд)
            winner = teamsAmount / 2;
            // Уменьшаем общее количество команд на количество сыгранных матчей
            teamsAmount -= matches_played;
            // Увеличиваем счетчик сыгранных матчей
            counter_matches += matches_played;
        }
        else {
            // Если количество команд нечетное
            // Вычисляем количество сыгранных матчей ((количество команд - 1) / 2)
            matches_played = (teamsAmount - 1) / 2;
            // Обновляем количество победителей (половина от общего количе-ства команд плюс одна команда)
            winner = ((teamsAmount - 1) / 2) + 1;
            // Уменьшаем общее количество команд на количество сыгранных матчей
            teamsAmount -= matches_played;
            // Увеличиваем счетчик сыгранных матчей
            counter_matches += matches_played;
        }
    }
    // Выводим информацию о количестве команд и сыгранных матчах
    cout << "Amount of teams = " << teamsAmount << ", Matches played = " << counter_matches;
}

 




Go
package main

import (
    "fmt"
)

// Функция countMatches принимает количество команд в турнире и воз-вращает количество матчей,
// которые должны быть сыграны в этом турнире.
func countMatches(n int) int {
    matches := 0 // Инициализируем переменную для хранения количества матчей

    // Пока количество команд больше 1
    for n > 1 {
        // Если количество команд четное
        if n%2 == 0 {
            matches += n / 2 // Добавляем половину количества команд к обще-му количеству матчей
            n /= 2           // Уменьшаем количество команд вдвое
        } else {
            matches += (n - 1) / 2 // Добавляем половину (n - 1) к общему коли-честву матчей
            n = (n - 1) / 2 + 1   // Устанавливаем количество команд в (n - 1) / 2 + 1
        }
    }

    return matches // Возвращаем общее количество матчей
}

func main() {
    var n int
    fmt.Println("Введите количество команд в турнире:")
    fmt.Scanln(&n) // Запрашиваем количество команд у пользователя
    fmt.Printf("Количество матчей: %d\n", countMatches(n)) // Выводим ре-зультат работы функции countMatches
}
 




Kotlin
// Функция countMatches вычисляет общее количество матчей в турнире по количеству команд.
fun countMatches(n: Int): Int {
    var matches = 0 // Переменная для хранения общего количества матчей
    var teams = n // Переменная для хранения текущего количества команд

    // Пока в турнире есть более одной команды
    while (teams > 1) {
        // Если количество команд четное
        if (teams % 2 == 0) {
            matches += teams / 2 // Добавляем половину количества команд к общему числу матчей
            teams /= 2 // Уменьшаем количество команд вдвое
        } else {	
            matches += (teams - 1) / 2 // Добавляем половину количества команд минус одну к общему числу матчей
            teams = (teams - 1) / 2 + 1 // Устанавливаем новое количество ко-манд (половина старого числа плюс одна)
        }
    }
    return matches // Возвращаем общее количество матчей
}

fun main() {
    val n = readLine()?.toIntOrNull() ?: return // Считываем количество ко-манд из ввода

    println("${countMatches(n)}") // Выводим результат работы функции countMatches
}
 

Задание 3.
Python
 Функция для переворота цифр числа
def reverse_digits(num):
    reversed_num = 0
    while num > 0:
        reversed_num = reversed_num * 10 + num % 10
        num //= 10	
    return reversed_num

 Функция для проверки увеличивающейся последовательности цифр в числе
def is_increasing(num):
    prev_digit = num % 10
    num //= 10
    while num > 0:
        digit = num % 10
        if digit >= prev_digit:
            return False
        prev_digit = digit
        num //= 10
    return True

 Функция для переворота и печати чисел, у которых цифры идут в воз-растающем порядке
def reverse_and_print_numbers(num_count):
     Проходим через указанное количество чисел
    for _ in range(num_count):
         Получаем число от пользователя
        num = int(input())
         Если цифры числа идут в возрастающем порядке
        if is_increasing(num):
             Переворачиваем число и выводим его
            print(reverse_digits(num), end=' ')

 Ввод количества чисел
num_count = int(input())
 Вызываем функцию для переворота и печати чисел
reverse_and_print_numbers(num_count)

 


Rust
use std::io::{self, BufRead};

fn reverse_number(mut num: u32) -> u32 {
    let mut reversed = 0;
    while num > 0 {
        reversed = reversed * 10 + num % 10;
        num /= 10;
    }
    reversed
}

fn is_decreasing_sequence(mut num: u32) -> bool {
    let mut prev_digit = num % 10;
    num /= 10;
    while num > 0 {
        let digit = num % 10;
        if digit >= prev_digit {
            return false;
        }
        prev_digit = digit;
        num /= 10;
    }
    true
}

fn main() {
    println!("Введите количество чисел:");
    let stdin = io::stdin();
    let mut input = String::new();
    stdin.lock().read_line(&mut input).expect("Ошибка чтения строки");
    let n: u32 = input.trim().parse().expect("Введено некорректное число");

    println!("Введите числа по одному:");
    for _ in 0..n {
        input.clear();
        stdin.lock().read_line(&mut input).expect("Ошибка чтения строки");
        let number: u32 = input.trim().parse().expect("Введено некорректное число");
        if is_decreasing_sequence(number) {
            print!("{} ", reverse_number(number));
        }
    }
}

 


Ruby
def reverse_numbers(sequence)
   Создаем строку для хранения перевернутых чисел
  reversed_numbers = ""

   Проходим по каждому числу в последовательности
  sequence.each do |num|
     Преобразуем число в строку
    num_str = num.to_s
     Проверяем, что цифры числа идут по возрастанию и что все цифры различны
    if num_str.chars.sort.join == num_str && num_str.chars.uniq.length != 1
       Если условие выполняется, добавляем перевернутое число в строку
      reversed_numbers << num_str.reverse + " "
    end
  end

   Возвращаем строку перевернутых чисел без пробелов в начале и конце
  return reversed_numbers.strip
end

 Пример использования:
puts "Введите последовательность чисел через пробел:"
 Получаем последовательность чисел от пользователя и преобразуем её в массив целых чисел
sequence = gets.chomp.split.map(&:to_i)
 Вызываем функцию и выводим результат
reversed = reverse_numbers(sequence)
puts "Числа из последовательности, у которых цифры идут по возраста-нию, в обратном порядке: {reversed}"
 
Java
import java.util.Scanner;

public class ReverseAscendingNumbers {
    public static void main(String[] args) {
        // Создаем объект Scanner для чтения ввода пользователя
        Scanner scanner = new Scanner(System.in);

        // Печатаем приглашение для пользователя ввести последовательность чисел
        System.out.println("Введите последовательность чисел через про-бел:");
        
        // Считываем введенную строку
        String input = scanner.nextLine();

        // Разделяем строку на числа по пробелам
        String[] numbers = input.split(" ");
        
        // Проходим по каждому числу в массиве чисел
        for (String number : numbers) {
            // Если число состоит из цифр, идущих по возрастанию
            if (isAscending(number)) {
                // Выводим перевернутое число
                System.out.print(reverseNumber(number) + " ");
            }
        }

        // Закрываем объект Scanner
        scanner.close();
    }

    // Проверка, является ли число составленным из цифр, идущих по воз-растанию
    public static boolean isAscending(String number) {
        // Проходим по каждой цифре в числе
        for (int i = 0; i < number.length() - 1; i++) {
            // Если текущая цифра больше или равна следующей цифре, число не идет по возрастанию
            if (number.charAt(i) >= number.charAt(i + 1)) {
                return false;
            }
        }
        // Если проверка не прервана, возвращаем true
        return true;
    }

    // Переворот числа
    public static String reverseNumber(String number) {
        // Создаем объект StringBuilder для построения перевернутой строки
        StringBuilder reversed = new StringBuilder();
        // Проходим по каждой цифре в обратном порядке
        for (int i = number.length() - 1; i >= 0; i--) {
            // Добавляем текущую цифру в начало строки
            reversed.append(number.charAt(i));
        }
        // Возвращаем перевернутую строку
        return reversed.toString();
    }
}

 

JavaScript
// Подключаем модуль readline для взаимодействия с пользователем через консоль
const readline = require('readline');

// Создаем интерфейс для чтения из стандартного потока ввода (input) и записи в стандартный поток вывода (output)
const rl = readline.createInterface({
  input: process.stdin,
  output: process.stdout
});

// Функция для переворачивания числа
function reverseNumber(num) {
  let reversed = 0;
  // Пока число больше нуля
  while (num > 0) {
    // Получаем последнюю цифру числа и добавляем ее в перевернутое число
    reversed = reversed * 10 + num % 10;
    // Убираем последнюю цифру числа
    num = Math.floor(num / 10);
  }
  return reversed;
}

// Функция для проверки, удовлетворяет ли число условиям задачи
function satisfiesCondition(num) {
  let prevDigit = 10;
  // Пока число больше нуля
  while (num > 0) {
    // Получаем последнюю цифру числа
    const digit = num % 10;
    // Если текущая цифра больше или равна предыдущей, число не удовле-творяет условию
    if (digit >= prevDigit) {
      return false;
    }
    // Запоминаем текущую цифру
    prevDigit = digit;
    // Убираем последнюю цифру числа
    num = Math.floor(num / 10);
  }
  return true;
}

let count;
let numbersProcessed = 0;

// Задаем вопрос пользователю: сколько чисел он собирается ввести
rl.question('', (input) => {
  count = parseInt(input);
  // Начинаем процесс ввода чисел
  askNumber();
});

function askNumber() {
  // Задаем вопрос пользователю: введите число
  rl.question('', (input) => {
    const num = parseInt(input);
    if (!isNaN(num)) {
      // Если введенное значение число, проверяем, удовлетворяет ли оно условию
      if (satisfiesCondition(num)) {
        // Если удовлетворяет, переворачиваем число и выводим его
        const reversed = reverseNumber(num);
        process.stdout.write(reversed + ' ');
      }
    }
    numbersProcessed++;
    // Проверяем, сколько чисел уже было обработано
    if (numbersProcessed < count) {
      // Если остались числа для ввода, задаем вопрос снова
      askNumber();
    } else {
      // Если все числа введены, закрываем интерфейс
      rl.close();
    }
  });
}
 

C
using System;

class Program
{
    // Функция для переворачивания числа
    static int ReverseNumber(int num)
    {
        int reversed = 0;
        // Пока число больше нуля
        while (num > 0)
        {
            // Добавляем последнюю цифру числа к перевернутому числу
            reversed = reversed * 10 + num % 10;
            // Удаляем последнюю цифру из числа
            num /= 10;
        }
        return reversed; // Возвращаем перевернутое число
    }

    // Функция для проверки, является ли последовательность цифр числа строго возрастающей
    static bool IsDigitsAscending(int num)
    {
        int lastDigit = num % 10;
        num /= 10;
        // Пока число больше нуля
        while (num > 0)
        {
            int currentDigit = num % 10;
            // Если текущая цифра больше или равна предыдущей, последова-тельность не является возрастающей
            if (currentDigit >= lastDigit)
            {
                return false;
            }
            lastDigit = currentDigit; // Обновляем предыдущую цифру
            // Удаляем последнюю цифру из числа
            num /= 10;
        }
        return true; // Возвращаем true, если последовательность возрастаю-щая
    }

    static void Main(string[] args)
    {
        Console.WriteLine("Введите количество чисел:");
        // Считываем количество чисел из ввода
        if (!int.TryParse(Console.ReadLine(), out int count))
        {
            Console.WriteLine("Ошибка при вводе количества чисел.");
            return;
        }

        Console.WriteLine($"Введите {count} чисел, разделенных пробелом:");
        // Считываем числа, разделенные пробелом, из ввода
        string[] numbers = Console.ReadLine()?.Split(' ');

        Console.WriteLine("Результат:");
        // Проходим по каждому введенному числу
        foreach (string number in numbers)
        {
            // Пытаемся преобразовать строку в число
            if (int.TryParse(number, out int num) && IsDigitsAscending(num))
            {
                // Если последовательность цифр в числе строго возрастающая, переворачиваем число и выводим результат
                int reversed = ReverseNumber(num);
                Console.Write($"{reversed} ");
            }
        }
    }
} 

Swift
// Функция для переворачивания числа
func reverseNumber(_ num: Int) -> Int {
    var number = num
    var reversed = 0
    // Пока число больше нуля
    while number > 0 {
        // Получаем последнюю цифру числа и добавляем ее в перевернутое число
        reversed = reversed * 10 + number % 10
        // Убираем последнюю цифру числа
        number /= 10
    }
    return reversed
}

// Функция для проверки, является ли последовательность цифр в числе строго возрастающей
func isIncreasingSequence(_ num: Int) -> Bool {
    var number = num
    var prevDigit = number % 10
    number /= 10
    // Пока число больше нуля
    while number > 0 {
        // Получаем текущую цифру числа
        let digit = number % 10
        // Если текущая цифра больше или равна предыдущей, последова-тельность не является возрастающей
        if digit >= prevDigit {
            return false
        }
        // Запоминаем текущую цифру
        prevDigit = digit
        // Убираем последнюю цифру числа
        number /= 10
    }
    return true
}

// Функция для вывода перевернутых уникальных чисел из последователь-ности
func printReversedNumbers() {
    // Выводим приглашение для пользователя ввести количество чисел
    print("Введите количество чисел:")
    // Считываем введенное пользователем значение
    guard let countInput = readLine(), let count = Int(countInput) else {
        print("Ошибка: введите целое число")
        return
    }
    
    // Выводим приглашение для пользователя ввести числа по одному
    print("Введите числа по одному:")
    var numbers = [Int]()
    // Считываем введенные пользователем числа и добавляем их в массив
    for _ in 0..<count {
        guard let numberInput = readLine(), let number = Int(numberInput) else {
            print("Ошибка: введите целое число")
            return
        }
        numbers.append(number)
    }
    
    // Проходим по каждому числу из массива
    for number in numbers {
        // Проверяем, является ли число возрастающей последовательностью
        if isIncreasingSequence(number) {
            // Если число удовлетворяет условию, переворачиваем его
            let reversed = reverseNumber(number)
            var digits = Set<Int>()
            var temp = reversed
            var isUnique = true
            // Проверяем, уникальны ли цифры в перевернутом числе
            while temp > 0 {
                let digit = temp % 10
                if digits.contains(digit) {
                    isUnique = false
                    break
                }
                digits.insert(digit)
                temp /= 10
            }
            // Если все цифры уникальны, выводим перевернутое число
            if isUnique {
                print(reversed, terminator: " ")
            }
        }
    }
}

// Пример использования функции
printReversedNumbers()

 
C++
include <iostream>
include <vector>

using namespace std;

// Функция для переворачивания числа
int reverseNumber(int number) {
    int reversed = 0;
    // Пока число не равно нулю
    while (number != 0) {
        // Получаем последнюю цифру числа
        int lastDigit = number % 10;
        // Добавляем ее к перевернутому числу
        reversed = reversed * 10 + lastDigit;
        // Удаляем последнюю цифру числа
        number /= 10;
    }
    return reversed;
}

// Функция для проверки, является ли последовательность цифр в числе строго возрастающей
bool isIncreasingDigits(int number) {
    int lastDigit = number % 10;
    number /= 10;
    // Пока число больше нуля
    while (number > 0) {
        // Получаем текущую цифру числа
        int currentDigit = number % 10;
        // Если текущая цифра больше или равна предыдущей, последова-тельность не является возрастающей
        if (currentDigit >= lastDigit)
            return false;
        lastDigit = currentDigit;
        // Удаляем последнюю цифру числа
        number /= 10;
    }
    return true;
}

int main()
{
    int n;
    // Запрашиваем количество входящих чисел
    cout << "Введите количество входящих чисел: ";
    cin >> n;

    vector<int> numbers(n);
    // Запрашиваем входящие числа
    cout << "Введите числа через пробел: ";
    for (int i = 0; i < n; ++i) {
        cin >> numbers[i];
    }

    // Проходим по каждому входящему числу
    cout << "Перевернутые числа для возрастающих последовательностей цифр: ";
    for (int number : numbers) {
        // Если последовательность цифр в числе строго возрастающая
        if (isIncreasingDigits(number) == true) {
            // Выводим перевернутое число
            cout << reverseNumber(number) << " ";
        }
    }
    cout << endl;
    return 0;
}

 
Go
package main

import (
	"fmt"
)

// Функция reverseNumber переворачивает заданное число.
func reverseNumber(num int) int {
	reversed := 0
	for num > 0 {
		reversed = reversed*10 + num%10 // Получаем последнюю циф-ру числа и добавляем ее к перевернутому числу
		num /= 10                       // Удаляем последнюю цифру числа
	}
	return reversed
}

// Функция isDecreasingSequence проверяет, является ли последователь-ность цифр числа строго убывающей.
func isDecreasingSequence(num int) bool {
	prevDigit := num % 10 // Получаем последнюю цифру числа
	num /= 10            // Удаляем последнюю цифру числа
	for num > 0 {
		digit := num % 10 // Получаем текущую цифру числа
		if digit >= prevDigit {
			return false // Если текущая цифра больше или равна предыдущей, последовательность не является убывающей
		}
		prevDigit = digit // Обновляем предыдущую цифру
		num /= 10        // Удаляем последнюю цифру числа
	}
	return true // Возвращаем true, если последовательность убывающая
}

func main() {
	var n, number int
	fmt.Println("Введите количество чисел:")
	fmt.Scan(&n) // Запрашиваем количество чисел у пользователя
	fmt.Println("Введите числа по одному:")
	for i := 0; i < n; i++ {
		fmt.Scan(&number) // Запрашиваем число у пользователя
		if isDecreasingSequence(number) {
			fmt.Printf("%d ", reverseNumber(number)) // Выводим пе-ревернутое число, если последовательность убывающая
		}
	}
}

 
Kotlin
// Функция reverseNumber переворачивает заданное число.
fun reverseNumber(num: Int): Int {
    var number = num // Создаем копию входного числа
    var reversed = 0 // Инициализируем переменную для хранения перевер-нутого числа
    // Пока число больше нуля
    while (number > 0) {
        reversed = reversed * 10 + number % 10 // Умножаем текущее перевер-нутое число на 10 и добавляем последнюю цифру в число
        number /= 10 // Удаляем последнюю цифру из числа
    }
    return reversed // Возвращаем перевернутое число
}

// Функция isIncreasingSequence проверяет, является ли последовательность цифр числа строго возрастающей.
fun isIncreasingSequence(num: Int): Boolean {
    var number = num // Создаем копию входного числа
    var prevDigit = number % 10 // Получаем последнюю цифру числа
    number /= 10 // Удаляем последнюю цифру из числа
    // Пока число больше нуля
    while (number > 0) {
        val digit = number % 10 // Получаем текущую цифру числа
        // Если текущая цифра больше или равна предыдущей, последова-тельность не является возрастающей
        if (digit >= prevDigit) {
            return false
        }
        prevDigit = digit // Обновляем предыдущую цифру
        number /= 10 // Удаляем последнюю цифру из числа
    }
    return true // Возвращаем true, если последовательность возрастающая
}

// Функция printReversedNumbers печатает перевернутые числа, удовле-творяющие условию возрастающей последовательности.
fun printReversedNumbers(count: Int, vararg numbers: Int) {
    // Проходим по каждому входному числу
    for (i in 0 until count) {
        val number = numbers[i] // Получаем текущее число
        // Если последовательность цифр в числе строго возрастающая
        if (isIncreasingSequence(number)) {
            val reversed = reverseNumber(number) // Переворачиваем число
            print("$reversed ") // Печатаем перевернутое число
        }
    }
}

fun main() {
    val count = readLine()?.toIntOrNull() ?: return // Считываем количество чисел из ввода

    val input = readLine() // Считываем числа через пробел
    if (input != null) {
        val nums = input.split(" ").mapNotNull { it.toIntOrNull() } // Разбиваем строку на числа и преобразуем их в список
        printReversedNumbers(count, *nums.toIntArray()) // Вызываем функ-цию печати перевернутых чисел
    }
}
 

Haskell
-- Функция для проверки, является ли число составленным из цифр, иду-щих по возрастанию
isIncreasingDigits :: Int -> Bool
isIncreasingDigits number = isIncreasingHelper (show number) '0'

-- Вспомогательная функция для проверки, является ли строка числа со-ставленной из цифр, идущих по возрастанию
isIncreasingHelper :: String -> Char -> Bool
isIncreasingHelper [] _ = True -- Пустая строка считается составленной из цифр, идущих по возрастанию
isIncreasingHelper (x:xs) prev
    | x <= prev = False -- Если текущая цифра не больше предыдущей, стро-ка не удовлетворяет условию
    | otherwise = isIncreasingHelper xs x -- Рекурсивный вызов для оставших-ся цифр

-- Функция для переворачивания числа
reverseNumber :: Int -> Int
reverseNumber number = reverseHelper number 0
    where
        reverseHelper 0 acc = acc -- Когда число становится нулем, возвраща-ется накопленный результат
        reverseHelper num acc = reverseHelper (num `div` 10) (acc * 10 + num `mod` 10)

-- Функция для обработки ввода и вывода результата
processInput :: [Int] -> IO ()
processInput [] = return () -- Если список пуст, завершить выполнение
processInput (x:xs) = do
    if isIncreasingDigits x
        then putStrLn (show (reverseNumber x)) -- Если число удовлетворяет условию, вывести его, перевернув
        else return () -- Если число не удовлетворяет условию, пропустить его
    processInput xs -- Рекурсивный вызов для остальных чисел

main :: IO ()
main = do
    putStrLn "Введите последовательность чисел:"
    input <- getLine -- Считать строку ввода
    let numbers = map read (words input) :: [Int] -- Преобразовать строку в список чисел
    processInput numbers -- Обработать введенные числа
 

Вывод
В результате данной лабораторной работы по программированию были выполнены все поставленные цели и задачи, нацеленные на изучение функций ввода-вывода данных, программирования вычисления значения выражения на различных языках программирования.
