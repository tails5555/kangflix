---
layout: post
title: "특수 정렬 알고리즘"
date: 2019-07-04 16:00:00 +09:00
image: "/kangflix/assets/img/category/ct_algorithm.png"
category: 'algorithm'
tags:
- Algorithm
- Sorting
description: 정수들에 강한 특수 정렬 알고리즘에 대해 알아봅니다.
introduction: 정수들에 강한 특수 정렬 알고리즘에 대해 알아봅니다.
---

정렬 알고리즘을 시간 복잡도가 O(N) 와 가깝게 구현할 수 있습니다.

그렇지만 임시 공간을 마련해야 하기 때문에 공간 복잡도가 O(N) 을 차지하게 됩니다.

이번 장에서는 시간 복잡도가 O(N + ?) 에 해당 되는 정렬 알고리즘에 대해 포스팅 하겠습니다.

# Counting Sort

![Counting_Sort_Anim]({{ site.baseurl }}/assets/img/post/algorithm/special_sort/counting_sort_anim.gif){: width="250px"}

- 배열에 들어간 숫자의 개수를 카운팅 하기 위한 배열을 생성해야 하기 때문에 공간 복잡도는 O(N) 만큼 나옵니다.
- 그렇지만 배열이 아니라 Java 의 `Map` 혹은 Python 의 `Directory` 를 사용하면 공간 복잡도를 최소화 할 수 있습니다.
- 그 대신 시간 복잡도는 O(N) 만큼 작동하는 만큼 속도는 매우 빠릅니다.
- 하지만 Integer 이외에 인덱스를 이루지 않는 변수 혹은 객체로 카운팅 정렬을 구현하기 힘든 단점이 있습니다.
- Java 에선 배열 인덱스를 음수로 못 쓰기 때문에 최솟값으로 가공 처리해야 합니다.
- 값들의 종류가 적을수록 이 정렬 방식을 사용하는 것이 좋습니다.

소스 코드는 아래와 같습니다.

```java
import java.util.Arrays;
import java.util.HashMap;
import java.util.Map;
import java.util.Random;

public class CountingSort {
    static final int SIZE = 30, BOUND = 500;
    static void counting_sort_array(int[] array){
        int max = Integer.MIN_VALUE;
        int min = Integer.MAX_VALUE;
        for(int k = 0; k < array.length; k++) {
            max = Math.max(max, array[k]);
            min = Math.min(min, array[k]);
        }

        int count_size = max - min + 1;
        int[] counting = new int[count_size];
        for(int k = 0; k < array.length; k++)
            counting[array[k] - min] += 1;

        for(int n = 1; n < counting.length; n++)
            counting[n] += counting[n - 1];

        int[] tmp = new int[array.length];
        for(int k = 0; k < array.length; k++){
            int index = counting[array[k] - min] - 1;
            tmp[index] = array[k];
            counting[array[k] - min] -= 1;
        }

        for(int k = 0; k < array.length; k++){
            array[k] = tmp[k];
        }
    }

    static void counting_sort_map(int[] array){
        int max = Integer.MIN_VALUE;
        int min = Integer.MAX_VALUE;
        for(int k = 0; k < array.length; k++) {
            max = Math.max(max, array[k]);
            min = Math.min(min, array[k]);
        }

        Map<Integer, Integer> counting = new HashMap<>();
        for(int k = 0; k < array.length; k++){
            int cnt = counting.getOrDefault(array[k], 0);
            counting.put(array[k], cnt + 1);
        }

        int[] ele_set = counting.keySet().stream().sorted().mapToInt(Integer::intValue).toArray();
        for(int k = 1; k < ele_set.length; k++){
            int before_cnt = counting.get(ele_set[k - 1]);
            int now_cnt = counting.get(ele_set[k]);
            counting.put(ele_set[k], before_cnt + now_cnt);
        }

        int[] tmp = new int[array.length];
        for(int k = 0; k < array.length; k++){
            int index = counting.get(array[k]) - 1;
            tmp[index] = array[k];
            counting.put(array[k], counting.get(array[k]) - 1);
        }

        for(int k = 0; k < array.length; k++){
            array[k] = tmp[k];
        }
    }

    public static void main(String[] args) {
        Random random = new Random();

        int[] rand_array1 = new int[SIZE];
        for(int k = 0; k < SIZE; k++){
            rand_array1[k] = random.nextInt(BOUND) + 1;
        }
        counting_sort_array(rand_array1);
        System.out.println(Arrays.toString(rand_array1));

        int[] rand_array2 = new int[SIZE];
        for(int k = 0; k < SIZE; k++){
            rand_array2[k] = random.nextInt(BOUND) - 250;
        }
        counting_sort_map(rand_array2);
        System.out.println(Arrays.toString(rand_array2));
    }
}
```

# Radix Sort

![Radix_Sort_Image]({{ site.baseurl }}/assets/img/post/algorithm/special_sort/radix_sort_image.png){: width="250px"}

- 낮은 자리수 부터 비교하여 정렬하는 것이 기본 정석입니다.
- 비교 연산이 전혀 필요 없습니다.
- 카운팅 정렬을 같이 사용하면 시간 복잡도는 O(d * n) 이 나옵니다. (d 는 진수 별 가장 큰 자리 수.)
- 공간 복잡도는 O(d + n).
- 흩어진 정수들을 정렬하는데 있어 매우 효율적인 알고리즘.
- 부동 소숫점 등 특수 비교 연산이 필요한 데이터는 무용지물.
- 진수 (10 진수, 16 진수 같은 거.) 가 클수록 반복 루프 횟수는 줄어들지만, 실행 메모리를 더 잡아 먹는 단점도 고려해야 합니다.

소스 코드는 아래와 같습니다.

```java
import java.util.Arrays;
import java.util.Random;

public class RadixSort {
    static final int SIZE = 30, MIN_BOUND = 100000, MAX_BOUND = 1000000;
    static Random random;
    static int[] array;

    static void counting_sort_decimal(int[] array, int pivot) {
        int[] counting = new int[10];

        for(int k = 0; k < array.length; k++) {
            int digit = (array[k] / pivot) % 10;
            counting[digit] += 1;
        }

        for(int k = 1; k < 10; k++)
            counting[k] += counting[k - 1];

        int[] tmp = new int[array.length];
        for(int k = array.length - 1; k >= 0; k--){
            int digit = (array[k] / pivot) % 10;
            int index = counting[digit] - 1;
            tmp[index] = array[k];
            counting[digit] -= 1;
        }

        for(int k = 0; k < array.length; k++)
            array[k] = tmp[k];
    }

    static void radix_sort_decimal(int[] array){
        int log10 = (int) Math.log10(MAX_BOUND);
        int pivot = 1;
        for(int d = 0; d < log10; d++) {
            counting_sort_decimal(array, pivot);
            pivot *= 10;
        }
    }

    static void initialize(){
        random = new Random();
        array = new int[SIZE];
        for(int k = 0; k < SIZE; k++)
            array[k] = random.nextInt(MAX_BOUND - MIN_BOUND) + MIN_BOUND;
    }

    public static void main(String[] args){
        initialize();
        radix_sort_decimal(array);
        System.out.println(Arrays.toString(array));
    }
}
```