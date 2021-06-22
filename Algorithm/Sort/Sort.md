``` java
public class Main {
    public static void main(String[] args) {
        int[] array = {10, 9, 8, 7, 6, 5, 4, 3, 2, 1};
        print(array);
        quickSort(array);
        print(array);
    }

    // 분할 정복, 추가 배열 필요 x, 정렬된 배열에 대해서는 오히려 시간이 많이 소요, 시간 복잡도 - O(nlogn)
    private static void quickSort(int[] array) {
        quickSort(array, 0, array.length - 1);
    }

    private static void quickSort(int[] array, int begin, int end) {
        int pivot = partition(array, begin, end);

        if (begin < pivot - 1) {
            quickSort(array, begin, pivot - 1);
        }

        if (pivot < end) {
            quickSort(array, pivot, end);
        }
    }

    private static int partition(int[] array, int begin, int end) {
        int mid = (begin + end) / 2;

        int left = begin;
        int right = end;

        while (left <= right) {
            while (array[left] < array[mid]) left++;

            while (array[right] > array[mid]) right--;

            if (left <= right) {
                swap(array, left, right);
                left += 1;
                right -= 1;
            }
        }

        return left;
    }

    // 분할 정복, 추가 배열 필요, 안정적, 시간 복잡도 - O(nlogn)
    private static void mergeSort(int[] array) {
        int[] helper = new int[array.length];
        mergeSort(array, helper, 0, array.length - 1);
    }

    private static void mergeSort(int[] array, int[] helper, int begin, int end) {
        if (begin < end) {
            int mid = (begin + end) / 2;

            mergeSort(array, helper, begin, mid);
            mergeSort(array, helper, mid + 1, end);
            merge(array, helper, begin, mid, end);
        }
    }

    private static void merge(int[] array, int[] helper, int begin, int mid, int end) {
        int index = begin;
        int left = begin;
        int right = mid + 1;

        for (int i = begin; i <= end; i++) {
            helper[i] = array[i];
        }

        while (left <= mid && right <= end) {
            if (helper[left] < helper[right]) {
                array[index] = helper[left];
                left += 1;
            } else {
                array[index] = helper[right];
                right += 1;
            }
            index += 1;
        }

        while (left <= mid) {
            array[index] = helper[left];
            index += 1;
            left += 1;
        }
    }



    // 추가배열 사용 x, 안정적, 시간복잡도 - O(n^2)
    private static void insertionSort(int[] array) {
        for (int i = 0; i <= array.length - 1; i++) {
            for (int j = i; j > 0; j--) {
                if (array[j] < array[j - 1]) {
                    swap(array, i, j);
                } else {
                    break;
                }
            }
        }
    }

    // 추가 배열 사용 x, 안정적 x, 시간복잡도 -  - O(n^2)
    private static void selectionSort(int[] array) {
        for (int i = array.length - 1; i > 0; i--) {
            int indexMax = 0;

            for (int j = 1; j <= i; j++) {
                if (array[j] > array[indexMax]) {
                    indexMax = j;
                }
            }

            swap(array, indexMax, i);
        }
    }

    // 추가 배열 사용 필요 x, 안정적, 시간복잡도 - O(n^2)
    private static void bubbleSort(int[] array) {
        for (int i = array.length - 1; i > 0; i--) {
            for (int j = 0; j <= i - 1; j++) {
                if (array[j] > array[j + 1]) {
                    swap(array, j, j + 1);
                }
            }
        }
    }

    private static void swap(int[] array, int index1, int index2) {
        int temp = array[index1];
        array[index1] = array[index2];
        array[index2] = temp;
    }

    private static void print(int[] array) {
        for (int i = 0; i < array.length; i++) {
            System.out.print(array[i] + " ");
        }
        System.out.println();
    }
}
```
