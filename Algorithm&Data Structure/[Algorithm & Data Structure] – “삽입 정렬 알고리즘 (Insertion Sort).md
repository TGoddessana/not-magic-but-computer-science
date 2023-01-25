---
title: "[Algorithm & Data Structure] – “삽입 정렬 알고리즘 (Insertion Sort)”"
date: "2023-01-25"
categories: 
  - "algorithm"
  - "computer-science"
  - "planguages"
  - "python"
  - "realpython"
tags: 
  - "algorithm"
  - "python"
  - "삽입정렬"
  - "알고리즘"
  - "정렬알고리즘"
---

[원본 글](https://gdsanadev.com/planguages/algorithm-data-structure-%ec%82%bd%ec%9e%85-%ec%a0%95%eb%a0%ac-%ec%95%8c%ea%b3%a0%eb%a6%ac%ec%a6%98-insertion-sort/)

## 삽입 정렬(Insertion sort) 이란?

**삽입 정렬은 자료 배열의 모든 요소를 앞에서부터 차례대로 이미 정렬된 배열 부분과 비교하여, 자신의 위치를 찾아 삽입함으로서 정렬을 완성하는 알고리즘입니다.**

## 문제 상황

숫자가 적혀 있는 카드들 5장이 있습니다. 각 카드들에 들어있는 숫자가 리스트로 주어질 때, 리스트 안에 있는 숫자들을 작은 수부터 큰 수 순서대로 정렬하세요.

## 구현

위의 카드 문제를 생각해 보겠습니다. 지금 제 책상에는 카드 5장이 놓여있습니다. 그리고 그러한 숫자들은 파이썬의 list 안에 저장될 수 있죠? 예시로, \[1,8,5,2,7\] 이 있다고 가정하겠습니다.

삽입 정렬은 **자료 배열의 모든 요소를 앞에서부터 차례대로 이미 정렬된 배열 부분과 비교하여, 자신의 위치를 찾아 삽입함으로서 정렬을 완성하는 알고리즘** 이라고 소개했습니다. 왼손은 비어 있고, 카드가 탁자 위에 뒤집힌 채 쌓여 있다고 가정합시다. 탁자에서 카드를 한 장씩 가져와 왼손의 적절한 위치에 삽입한다고 생각해 봅시다. 카드가 삽입될 적절한 위치를 알아내려면, 왼손에 이미 든 카드를 오른쪽부터 왼쪽으로 가며 비교해보면 됩니다. 이때 왼손에 들고 있던 카드들은 모두 정렬된 카드들입니다. 삽입 정렬의 아이디어를 `Python` 코드로 나타낸다면, 아래와 같습니다. 아래의 코드에서, 입력 배열 `array` 는 정렬된 출력 수열로 변환됩니다.

```python
def insertion_sort(array):
    for current_index in range(1, len(array)):
        current_value = array[current_index]
        # current_index 이전의 index 는 이미 정렬된 요소들의 index
        sorted_index = current_index - 1
        # sorted_index 가 양의 정수이고, 현재 요소의 값이 이미 정렬된 요소의 값보다 작으면,
        while sorted_index >= 0 and current_value < array[sorted_index]:
            # 이미 정렬된 요소를 오른쪽으로 한 칸 밀고,
            array[sorted_index + 1] = array[sorted_index]
            # 이미 정렬된 index 값을 1 감소
            sorted_index = sorted_index - 1
        array[sorted_index + 1] = current_value  # 현재 요소의 값이 이미 정렬된 요소의 값보다 크면, 현재 요소를 배열의 맨 마지막에 삽입
       
```

`insertion_sort` 라는 함수 하나를 정의했습니다.

- 2번 줄의 `current_index` 는 왼손으로 가져가 정렬할 현재 카드를 나타냅니다.

- 2번째 줄의 `for current_index in range(1, len(array)):` 가 시작될 때, 부분 배열인 `array[0] ~ array[sorted_index]` 는 현재 손에 쥔 정렬된 카드를, 나머지 부분 배열인 `array[current_inex+1] ~ array[len(array)]` 는 아직 탁자에 쌓여있는 카드를 나타냅니다.

- 즉, `array[0] ~ array[sorted_index]` 는 처음에 탁자에 쌓인 순서대로 맨 앞부터 `array[sorted_index]` 까지의 값이지만 이제는 정렬되어 저장된 것입니다.

- 위와 같은 특성을, 엄밀하게 표현하면 루프 불변성이라고 합니다. 그렇다면 루프 불변성이란 무엇일까요?

## 루프 불변성

위의 코드가 작동하는 과정을 한 줄씩 뜯어봅시다. 정의된 `insertion_sort` 함수에 `[1,8,5,2,7]` 을 넣어보겠습니다.

```python
if __name__ == "__main__":
    array = [1, 8, 5, 2, 7]
    insertion_sort(array=array)
    print(array)
```

```python
[1, 8, 5, 2, 7]
```

첫 번째 for 반복이 시작될 때, `array` 는 위와 같습니다.

![](https://gdsanadev.com/wp-content/uploads/2023/01/스크린샷-2023-01-26-오전-12.40.25-1024x55.png)

![](https://gdsanadev.com/wp-content/uploads/2023/01/스크린샷-2023-01-26-오전-12.41.38-1024x62.png)

그리고 `current_index` 에는 1이 담기고, `current_value` 에는 두 번째 값인 8이 담깁니다.

![](https://gdsanadev.com/wp-content/uploads/2023/01/image-130-1024x51.png)

다음의 코드인 sorted\_index 에는 `0` 이 담기겠네요.

![](https://gdsanadev.com/wp-content/uploads/2023/01/스크린샷-2023-01-26-오전-12.43.22-1024x96.png)

그리고 이미 정렬된 숫자인 `1` 보다 반복문에서의 현재 값이 크므로, 위의 조건에 부합하지 않아 while 반복문은 수행되지 않습니다.

![](https://gdsanadev.com/wp-content/uploads/2023/01/image-132-1024x102.png)

단지 현재 값을 두 번째 요소로서 넣어줄 뿐이죠. 위의 과정이 수행되고 나면, `array` 는 아래와 같을 겁니다. 아직은 변한 게 없네요.

```python
[1, 8, 5, 2, 7]
```

![](https://gdsanadev.com/wp-content/uploads/2023/01/스크린샷-2023-01-26-오전-12.49.45-1024x99.png)

좋아요. 다시 for 반복이 시작되고 `current_index` 에는 2와 5가 담깁니다. 1과 8은 이미 왼손에 정렬된 상태로 잡고 있고, 이제 오른손에는 카드 5를 들고 있는 상황입니다.

![](https://gdsanadev.com/wp-content/uploads/2023/01/image-133-1024x84.png)

이제 가장 큰 8부터, 그러니까 오른쪽부터 왼쪽으로 가면서 하나하나 비교해 보면 되겠네요. `current_value` 는 5이고, `array[sorted_index]` 는 8입니다. 5가 더 작으므로, `array[sorted_index+1]` 에는 `array[sorted_index]` 가 담깁니다. 왼손에 쥔 두 개의 카드, 1과 8 사이를 넓게 벌려 공간을 준 것과 같습니다.

![](https://gdsanadev.com/wp-content/uploads/2023/01/image-134.png)

`array` 에는 값이 그대로 대입되므로 그 순간은 위와 같은 상황입니다.

![](https://gdsanadev.com/wp-content/uploads/2023/01/image-135-1024x291.png)

이후 이미 정렬된 index 값을 1 감소시키며, 내 앞에 있는 카드에 적혀 있는 숫자가 더 작나를 비교합니다. 오른쪽부터 카드 사이사이 공간을 벌려가며 어디에 끼워넣으면 좋을지를 판단합니다. 하지만, 이번 경우에는 현재 값인 5보다 `array[sorted_index]` 인 1이 더 작으므로, 우리의 함수는 "아 이 곳에 끼워넣으면 되겠네?" 를 판단하고 수행합니다.

![](https://gdsanadev.com/wp-content/uploads/2023/01/image-136-1024x120.png)

이런 방식으로 모든 카드를 반복합니다.

이러한 과정을 굳이 다시 한 번 짚고 넘어간 이유는 루프 불변성에 대해서 설명하기 위함이었습니다.

> In [computer science](https://en.wikipedia.org/wiki/Computer_science), a **loop invariant** is a property of a [program](https://en.wikipedia.org/wiki/Computer_program) [loop](https://en.wikipedia.org/wiki/Control_flow#Loops) that is true before (and after) each iteration.
> 
> 컴퓨터 과학에서 루프 불변성은 각 반복 전후에 참인 프로그램 루프의 속성입니다.
> 
> https://en.wikipedia.org/wiki/Loop\_invariant

원래 딱딱한 설명만 들으면 뭔가 싶고 포기하고 싶어집니다. 하지만 괜찮습니다. 쉽게만 살아가면 재미없습니다. 정의만 듣고 세상 모든 것을 이해할 수 있었다면, 삽질 한 번에 모든 것을 해결할 수 있었다면 즐거움이란 건 없었겠죠. 밤이 존재해야지만 낮이 그 특별함을 가지듯이, 우리가 겪는 어려움도 존재해야지만 해결했을 때에 그 즐거움과 특별함을 가질 수 있습니다. 가봅thㅣ다!

앞서 우리의 알고리즘이 동작하는 과정을 간략하게 살펴보면 반복이 나옵니다. for 루프로부터 시작하는 반복인데, 제대로 위의 과정들을 이해하셨다면 당연히 for 루프가 반복을 시작하는 시점에서는 이전 index 의 카드들이 모두 정렬된 상태로 저장된다는 사실 또한 이해하실 수 있을 것입니다.

위의 예시에서 **"`array[0] ~ array[sorted_index]` 부분 배열은 원래의 `array[0] ~ array[sorted_index]` 원소이지만, `for` 루프가 반복을 시작할 때마다 정렬된 순서로 구성된다"** 는 항상 참입니다. 이쯤에서 위의 정의를 다시 읽어봅시다. _루프 불변성은 각 반복 전후에 참인 프로그램 루프의 속성이다_ 라고 했었죠. 이곳에서 **속성은 반복 전 하위 배열이 무조건 정렬되어 있다는 사실입니다.** 루프 불변성은 알고리즘이 타당한 이유를 쉽게 이해할 수 있도록 하기 위해서 사용되는데, 우리는 위의 루프 불변성을 보임으로서 작성한 `insertion_sort` 함수가 타당함을 증명해 보겠습니다.

루프 불변성을 보이기 위해서는, 아래의 세 가지 특성을 만족해야 합니다.

1. (초기조건) 루프가 첫 번째 반복을 시작하기 전, 루프 불변성이 참이어야 한다.

3. (유지조건) 루프의 반복이 시작되기 전에 루프 불변성이 참이었다면 다음 반복이 시작되기 전까지도 계속 참이어야 한다.

5. (종료조건) 루프가 종료될 때 그 불변식이 알고리즘의 타당성을 보이는 데 도움이 될 유용한 특성을 가져야 한다.

이를 우리의 함수에 맞춰서 잠깐 바꿔볼까요?

1. (초기조건) 루프의 첫 반복이 시작되기 전, 즉 두 번째 카드부터 반복하기 전 루프 불변성이 성립하는지를 살펴보아야 합니다. "첫 반복이 시작되기 전 루프 불변성을 조사하는 시점" 은 루프 카운트 변수가 초기화된 직후 루프 헤더에서 첫 검사를 하기 직전을 의미합니다. 우리의 함수의 경우, 루프 카운트 변수는 `current_index` 이고, 이것에 1이 할당된 다음 그것이 `len(array)` 의 범위에 있는지를 검사하기 직전을 의미하겠네요. 이러한 경우 부분 배열인 `array[0] ~ array[sorted_index]` 는 한 개의 원소 `1` 로 구성되는데, 원래 `array[1]` 의 값이었죠. 그리고 정렬되어 있는 상태입니다. **루프의 반복 시작 전, 루프 불변성은 성립합니다.**

3. (유지조건) 루프의 반복이 시작되기 전 루프 불변성이 참이었다면 다음 반복이 시작되기 전까지도 계속 참이어야 합니다. 매 반복 시 루프 불변성이 유지되는지 (부분 배열이 항상 정렬된 상태로 유지되는지) 를 보여야 하는데, 위의 코드에서 `for` 루프의 바디 부분은 끼워넣을 카드의 올바른 위치를 찾을 때까지 손가락으로 카드 사이 사이 공간을 하나씩 벌려주는 역할을 합니다. - 오른쪽으로 한 자리씩 이동시키는 작업을 한다는 이야기입니다. 그리고 적절한 위치에 값을 삽입합니다. 그 결과로, 부분 배열 `array[0] ~ array[sorted_index]` 는 기존의(정렬되기 전의) 배열 `array[0] ~ array[sorted_index]` 과 동일한 원소를 정렬된 상태로 가지게 됩니다. `current_index` 가 1씩 증가하며 `for` 루프의 다음 반복에서도 루프 불변성이 유지됩니다.

5. (종료조건) 루프가 종료될 때 그 불변식(부분 배열이 정렬되어 있다는 것) 이 알고리즘의 타당성을 보이는 데에 도움이 되는 유용한 특성을 가지고 있어야 합니다. 위의 알고리즘의 경우 `for` 루프는 `current_index` 가 `range(1, len(array))` 의 범위에 있지 않을 때에 종료됩니다. 즉 `current_index = len(array)+1` 일 때에 종료됩니다. 2번 유지 조건에서, `current_index` 에 `len(array)+1` 을 대입해 본다면 `배열 array[0] ~ array[sorted_index]` 는 원래 `array[0] ~ array[sorted_index]` 의 원소로 구성되지만 정렬된 순서로 저장됨을 알 수 있습니다. (`sorted_index = current_index` 였음을 기억합시다!) **마지막 순간 배열 `array[0] ~ array[sorted_index]` 는 전체 배열이므로**, 배열 전체가 정렬되었으며 이는 우리의 알고리즘이 타당함을 의미합니다.

이렇게 간단하게 보이는 삽입 정렬 알고리즘의 기본적인 아이디어를 알아봤습니다. 또한 루프 불변성이라는 새로운 개념을 알아보며 그것을 증명함으로서 작성한 알고리즘이 타당함을 보였습니다. 굉장히 간단한 코드이고, 그것이 어떻게 동작하는지도 알고 있다고 생각했지만 - 증명하는 과정에서 "당연하게 사실" 이라고 여기던 것들을 사실이라고 과연 자신있게 말할 수 있는 논리력을 저는 지니고 있는가.. 에 대한 고찰을 하게 된 것 같습니다.
