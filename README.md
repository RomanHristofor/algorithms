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
        count += 1;
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
console.log('count', count);
```
