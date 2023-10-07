# Algorithms

# String
## Задача 1: Поиск наибольшей подстроки без повторяющихся символов
Описание:
Найти длину наибольшей подстроки в строке, в которой нет повторяющихся символов.
```
function findLongestSubstring(str) {
  let longest = 0;
  let left = 0;
  let right = 0;
  const map = new Set();

  while(right < str.length) {
    if(!map.has(str[right])) {
      map.add(str[right]);
      longest = Math.max(longest, right - left + 1); 
      right++;
    } else {
      map.delete(str[left]);
      left++;
    }
  }

  return longest;
}
findLongestSubstring("abcabcbb"); // Ожидаемый результат: 3 ("abc" - подстрока без повторений)
findLongestSubstring("bbbbb");   // Ожидаемый результат: 1 ("b" - подстрока без повторений)
```


## Задача 2: Палиндромы
Описание:
Палиндром - это слово, фраза, число или другая последовательность символов, которая читается одинаково
как слева направо, так и справа налево (без учета пробелов, знаков препинания и регистра).
Ваша задача - реализовать функцию isPalindrome(str), которая будет проверять, является ли данная строка палиндромом.
Требования:
Ваша функция должна игнорировать регистр символов и пробелы.
Ограничение по памяти O(1).
Допустимо использование регулярных выражений для удаления нежелательных символов.

```
function isPalindrome(str) {
    let first = 0;
    let end = str.length - 1;

    while(first < end) {
        const firstChar = str[first];
        const endChar = str[end];

        if (firstChar.toLowerCase() === firstChar.toUpperCase()) {
            first += 1;
            continue;
        }
        if (endChar.toLowerCase() === endChar.toUpperCase()) {
            end -= 1;
            continue;
        }

        if (firstChar.toLowerCase() !== endChar.toLowerCase()) {
            return false
        }
        
        first += 1;
        end -= 1;
    }
    return true;
}
isPalindrome("Do geese see God?"); // true
isPalindrome("А роза упала на лапу Азора"); // true
isPalindrome("Madam, I'm Adam"); // true
isPalindrome("hello"); // false
```


## Задача 3: Сбалансированы ли скобки в строке
Описание:
Дана строка состоящая из букв латинского алфавита, цифр и скобок {([])}.
Необходимо проверить что скобки в строке сбалансированы - на каждую открывающую скобку приходится закрывающая
и скобочные группы не пересекаются.
Напишите функцию которая принимает такую строку и возвращает true если скобки сбалансированы
и false если не сбалансированы.

```
function isValid(str) {
  const stack = [];
  const brackets = {
    ')': '(',
    '}': '{',
    ']': '['
  };

  for (let i = 0; i < str.length; i++) {
    const char = str[i];

    if ('{(['.includes(char)) {
      stack.push(char);
    }

    if ('})]'.includes(char)) {
      if (stack.length === 0) {
        return false;
      }

      const last = stack.pop();
      if (last !== brackets[char]) {
        return false;
      }
    }
  }
  return stack.length === 0;
}
isValid("(foo)"); // true
// isValid("(f[o]{o})"); // true
// isValid("[(){}()()]"); // true
// isValid("(foo"); // false
// isValid("{f[o}o]"); // false
```


## Задача 4: Найти наименьшую подстроку N, содержащая все символы K
Описание:
Пусть функция MinWindowSubstring принимает массив строк, который будет содержать
только две строки, первый параметр — строка N, а второй параметр — строка K некоторых символов,
И ваша цель — определить наименьший подстрока N, содержащая все символы K. 
Например: ["aaabaaddae", "aed"], то наименьшая подстрока N, содержащая символы a, e и d, — это "dae",
Другой пример: ["aabdccdbcacd", "aad"] , то наименьшая подстрока N, содержащая все символы из K
— это "aabd", расположенная в начале строки.

```
function minSubstring(strArr) {
  let A = strArr[1];
  let B = strArr[0];
  let minLength = Infinity;
  let minSubstring = "";

  for (let i = 0; i < B.length; i++) {
    for (let j = i + 1; j <= B.length; j++) {
      let subStr = B.slice(i, j);
      let isFound = true;
      let aChars = A.split('');

      for (let k = 0; k < aChars.length; k++) {
        let index = subStr.indexOf(aChars[k]);
        if (index !== -1) {
          subStr = subStr.slice(0, index) + subStr.slice(index + 1);
        } else {
          isFound = false;
          break;
        }
      }

      if (isFound && B.slice(i, j).length < minLength) {
        minLength = B.slice(i, j).length;
        minSubstring = B.slice(i, j);
      }
    }
  }
  return minSubstring;
}
minSubstring(["ahffaksfajeeubsne", "jefaa"]); // Output: aksfaje
```





# Array
## Задача: Поиск второго максимального числа в массиве
```
function findSecondMax(arr) {
  let firstMax = -Infinity;
  let secondMax = -Infinity;

  for (const num of arr) {
    if (num > firstMax) {
      secondMax = firstMax;
      firstMax = num;
    } else if (num > secondMax && num < firstMax) {
      secondMax = num;
    }
  }

  return secondMax;
}
findSecondMax([2, 3, 6, 6, 5]); // 5
```

## Задача: Быстрая сортировка элементов массива
Описание:
Реализовать функцию quickSort(arr), которая будет сортировать массив целых чисел с использованием алгоритма быстрой сортировки (QuickSort).
Требования:
Ваша функция должна использовать алгоритм быстрой сортировки для сортировки массива.
Алгоритм QuickSort работает по принципу выбора опорного элемента (pivot),
разделения массива на подмассивы меньших и больших элементов, и рекурсивной сортировки этих подмассивов.

```
function quickSort(arr) {
    if (arr.length <= 1) return arr;

    const pivot = arr[0];
    const left = [];
    const right = [];
    
    for(let i = 1; i < arr.length; i++) {
        if (arr[i] < pivot) {
            left.push(arr[i]);
        } else {
            right.push(arr[i]);
        }
    }
    return [...quickSort(left), pivot, ...quickSort(right)];
}
const unsortedArray = [8, 3, 9, 4, 6, 10, 2, 7, 5, 1];
console.log(quickSort(unsortedArray)); // Ожидаемый результат: [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]
```

## Задача: Бинарный поиск в отсортированном массиве
Описание:
Реализовать функцию binarySearch(arr, target), которая будет осуществлять поиск заданного элемента target в отсортированном
массиве arr методом бинарного поиска.
Требования:
1. Ваша функция должна использовать алгоритм бинарного поиска для нахождения элемента.
2.Массив arr должен быть отсортирован в порядке возрастания.
3. Если элемент найден, функция должна вернуть его индекс. Если элемент отсутствует в массиве, функция должна вернуть -1.

```
function binarySearch(arr, target) {
  let left = 0;
  let right = arr.length - 1;

  while (left <= right) {
    const mid = Math.floor((left + right) / 2);

    if (arr[mid] === target) {
      return mid;
    }

    if (arr[mid] < target) {
      left = mid + 1;
    } else {
      right = mid - 1;
    }
  }

  return -1;
}
const sortedArray = [1, 3, 5, 7, 9, 11, 13, 15];
const target = 7;
console.log(binarySearch(sortedArray, target)); // Выводит 3, так как элемент 7 находится в позиции с индексом 3
```

## Задача: Поиск уникального элемента в массиве
Описание:
Вам нужно реализовать функцию findUnique(arr), которая принимает массив целых чисел,
в котором каждое число повторяется дважды, кроме одного числа, которое встречается только один раз.
Ваша задача - найти это уникальное число.
Требования:
Ваше решение должно иметь временную сложность O(n) и не использовать дополнительную память, кроме константного объема.
```
function findUnique(arr) {
  let unique = 0;
  
  for (const num of arr) {
    unique ^= num; // Применение операции XOR
  }
  return unique;
}
console.log(findUnique([4, 5, 6, 3, 4, 5, 6])); // Ожидаемый результат: 3

function findUnique(arr) {
  const countMap = {}; 
  
  for (const num of arr) {
     if (countMap[num]) {
       countMap[num]++;
     } else {
       countMap[num] = 1;
     }
  }

  let minKey = null;
  let minVal = Infinity;

  for (const key in countMap) {
    if (countMap[key] < minVal) {
      minVal = countMap[key];
      minKey = parseInt(key);
    }
  }
  return minKey;
}
findUnique([4, 5, 6, 7, 4, 5, 6]); // 7
```

## Задача: Сортировка слиянием
Описание:
Вам нужно реализовать функцию mergeSort(arr), которая будет сортировать массив целых чисел методом слияния.
const unsortedArray = [8, 3, 9, 4, 6, 10, 2, 7, 5, 1];
// Ожидаемый результат: [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]
Требования:
Ваша функция должна использовать метод слияния (merge sort) для сортировки массива.
Реализуйте алгоритм рекурсивно.

```
function merge(left, right) {
    const res = [];
    let leftIdx = 0;
    let rightIdx = 0;

    while(leftIdx < left.length && rightIdx < right.length) {
        if (left[leftIdx] < right[rightIdx]) {
            res.push(left[leftIdx]);
            leftIdx++;
        } else {
            res.push(right[rightIdx]);
            rightIdx++;
        }
    }
    return res.concat(left.slice(leftIdx)).concat(right.slice(rightIdx));
}

function mergeSort(arr) {
    if (arr.length <= 1) return arr;

    const mid = Math.floor(arr.length / 2);
    const left = arr.slice(0, mid);
    const right = arr.slice(mid);
    
    return merge(mergeSort(left), mergeSort(right));
}
mergeSort(unsortedArray);
```

## Задача: Объединение интервалов
Описание:
Дан массив интервалов, представленных в виде массивов [start, end], где start - начальное значение интервала,
а end - конечное значение интервала. 
Ваша задача - объединить перекрывающиеся интервалы и вернуть новый массив неперекрывающихся интервалов.
```
function mergeIntervals(intervals) {
  if (!intervals.length) return intervals;

  // Сортируем интервалы по стартовому значению
  intervals.sort((a, b) => a[0] - b[0]);

  const result = [intervals[0]];

  for (let i = 1; i < intervals.length; i++) {
    const currentInterval = intervals[i];
    const lastMergedInterval = result[result.length - 1];

    // Если текущий интервал пересекается с последним объединенным интервалом,
    // обновляем конечное значение последнего объединенного интервала
    if (currentInterval[0] <= lastMergedInterval[1]) {
      lastMergedInterval[1] = Math.max(currentInterval[1], lastMergedInterval[1]);
    } else {
      // Иначе добавляем текущий интервал в результат
      result.push(currentInterval);
    }
  }

  return result;
}
mergeIntervals([[1, 3], [2, 6], [8, 10], [15, 18]]); // Ожидаемый результат: [[1, 6], [8, 10], [15, 18]]
```


## Задача: 
Возьмем массив строк, хранящийся в strArr, который будет содержать пары целых чисел в следующем формате: (i1,i2), 
где i1 представляет дочерний узел в дереве, а второе целое число i2 означает, что он является родителем i1.
Например: если strArr равен `["(1,2)", "(2,4)", "(7,2)"]`, то это формирует правильное бинарное дерево.
В этом случае ваша программа должна возвращать строку true, потому что может быть сформировано действительное двоичное дерево.
Если правильное бинарное дерево не может быть сформировано из целочисленных пар, верните строку false.
Все целые числа в дереве будут уникальными, что означает, что в дереве может быть только один узел с заданным целочисленным значением.
```
function TreeConstructor(strArr) {
  let nodes = {};
  let parents = {};

  for (let i = 0; i < strArr.length; i++) {
    let pair = strArr[i].match(/\d+/g).map(Number);
    let child = pair[0];
    let parent = pair[1];

    if (nodes[child]) {
      return false;
    }

    nodes[child] = parent;

    if (!parents[parent]) {
      parents[parent] = 1;
    } else {
      parents[parent]++;
      if (parents[parent] > 2) {
        return false;
      }
    }
  }

  return true;
}
TreeConstructor(
    ["(1,2)", "(2,4)", "(5,7)", "(7,2)", "(9,5)"] // true
    ["(1,2)", "(3,2)", "(2,12)", "(5,2)"] // false
);
```


## Задача:
Пример реализации поиска в графе с использованием алгоритма поиска в ширину `BFS`
```
const graph = {};
graph.a = ['b', 'c'];
graph.b = ['f'];
graph.c = ['f'];
graph.o = ['d', 'e'];
graph.d = ['f'];
graph.f = ['g'];

function bfs(graph, start, end) {
  // Список посещенных вершин
  const visited = new Set();

  // Очередь вершин для обхода
  const queue = [];

  // Добавляем начальную вершину в очередь и помечаем ее как посещенную
  queue.push(start);
  visited.add(start);

  // Итеративно обходим граф
  while (queue.length > 0) {
    // Извлекаем первую вершину из очереди
    const node = queue.shift();

    // Проверяем, является ли текущая вершина целевой
    if (node === end) {
      return true;
    }

    // Добавляем все соседние вершины в очередь, если они еще не были посещены
    graph[node].forEach((neighbor) => {
      if (!visited.has(neighbor)) {
        queue.push(neighbor);
        visited.add(neighbor);
      }
    });
  }
  // Если целевая вершина не найдена, возвращаем false
  return false;
}
// Ищем путь от вершины 'a' к вершине 'g'
bfs(graph, 'a', 'g'); // true
```
