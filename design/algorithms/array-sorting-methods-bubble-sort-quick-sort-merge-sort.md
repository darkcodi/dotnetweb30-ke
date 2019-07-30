# Array sorting methods \(bubble sort, quick sort, merge sort\)

### Bubble sort

{% hint style="success" %}
**Bubble sort** is a simple sorting algorithm. This sorting algorithm is comparison-based algorithm in which each pair of adjacent elements is compared and the elements are swapped if they are not in order. This algorithm is not suitable for large data sets as its average and worst case complexity are of **Ο\(n2\)** where n is the number of items.
{% endhint %}

![bubble-short](https://softserveke.firebaseapp.com/assets/img/bubble-short.45f1eb10.png)

If the given array has to be sorted in ascending order, then bubble sort will start by comparing the first element of the array with the second element, if the first element is greater than the second element, it will swap both the elements, and then move on to compare the second and the third element, and so on.

**If we have total n elements, then we need to repeat this process for n-1 times.**

It is known as bubble sort, because with every complete iteration the largest element in the given array, bubbles up towards the last place or the highest index, just like a water bubble rises up to the water surface.

Sorting takes place by stepping through all the elements one-by-one and comparing it with the adjacent element and swapping them if required.

### Quick sort

{% hint style="success" %}
**QuickSort** is a Divide and Conquer algorithm. It picks an element as pivot and partitions the given array around the picked pivot. There are many different versions of quickSort that pick pivot in different ways.
{% endhint %}

> Основная идея заключается в том, чтобы найти опорный элемент в массиве для сравнения с остальными частями, затем сдвигать элементы так, чтобы все части перед опорным элементом были меньше его, а все элементы после опорного были больше его. После этого рекурсивно выполнить ту же операцию на элементы до и после опорного.

1. Always pick first element as pivot.
2. Always pick last element as pivot \(implemented below\)
3. Pick a random element as pivot.
4. Pick median as pivot.

The key process in quickSort is partition\(\). Target of partitions is, given an array and an element x of array as pivot, put x at its correct position in sorted array and put all smaller elements \(smaller than x\) before x, and put all greater elements \(greater than x\) after x. All this should be done in linear time.

Pseudo Code for recursive QuickSort function

```text
/* low  --> Starting index,  high  --> Ending index */
quickSort(arr[], low, high)
{
    if (low < high)
    {
        /* pi is partitioning index, arr[pi] is now
           at right place */
        pi = partition(arr, low, high);

        quickSort(arr, low, pi - 1);  // Before pi
        quickSort(arr, pi + 1, high); // After pi
    }
}
```

Основные шаги для разделения массива:

1. Найти опорный элемент в массиве. Этот элемент — основа для сравнения за одни проход.
2. Установить указатель \(левый указатель\) с первого элемента в массиве.
3. Установить указатель \(правый указатель\) с последнего элемента в массиве.
4. Пока значение левого указателя в массиве меньше, чем значение опорного элемента, сдвигать левый указатель вправо \(добавить 1\). Продолжить пока значение левого указателя не станет большим или равным опорному.
5. Пока значение правого указателя в массиве больше, чем значение опорного элемента, сдвигать правый указатель влево \(вычитать 1\). Продолжать пока значение правого указателя не станет меньшим или равным значению разделителя.
6. Если левый указатель меньше или равен правому указателю, поменять значения в этих местах в массиве.
7. Сдвинуть левый указатель вправо на одну позицию и правый указатель на одну позицию влево.
8. Если левый указатель и правый указатель не встретятся, перейти к шагу 1.

### Merge sort

1. Разбитие массива на мелкие части одинакового размера. Рекурсивно массив разбивается пока у нас не будет отдельных элементов
2. Сливаем части “соседних массивов” в один с сортировкой. Опять же, сортировка проходит достачтоно интересно: так как мы сливаем уже сортированные массивы — в результате хотелось бы получить сортированный массив. Итак, допустим у нас есть два массива:

2.1 Указатели указывают на первый элемент обоих массивов. Выбирается наименьший из них

2.2 В массиве в котором было наименьшее число — указатель переноситься на следующий элемент. Повторяем пункт 2.1

2.3 Если в одном из массивов закончились элементы — переносим элементы другого массива в наш отсортированный массив \( слив остатков \)

1. Повторяем пока подмасивы не закончатся

![merge-sort](https://softserveke.firebaseapp.com/assets/img/merge-sort.ed5e180d.gif)

