# Algorithms

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






