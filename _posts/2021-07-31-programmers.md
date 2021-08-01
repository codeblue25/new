---
layout: post
title: "[프로그래머스 / Python] Level 2 가장 큰 수"
date: 2021-08-01T15:25:52-05:00
author: codeblue25
categories: Algorithm
---

<h2>문제</h2>

0 또는 양의 정수가 주어졌을 때, 정수를 이어 붙여 만들 수 있는 가장 큰 수를 알아내 주세요. <br />
예를 들어, 주어진 정수가 [6, 10, 2]라면 [6102, 6210, 1062, 1026, 2610, 2106]를 만들 수 있고, 이중 가장 큰 수는 6210입니다.<br />
0 또는 양의 정수가 담긴 배열 numbers가 매개변수로 주어질 때, 순서를 재배치하여 만들 수 있는 가장 큰 수를 문자열로 바꾸어 return 하도록 solution 함수를 작성해주세요

<h2>제한사항</h2>

- numbers의 길이는 1 이상 100,000 이하입니다.
- numbers의 원소는 0 이상 1,000 이하입니다.
- 정답이 너무 클 수 있으니 문자열로 바꾸어 return 합니다.

<h2>🔹나의 풀이</h2>

<h3>첫번째 풀이</h3>

```python
def solution(lst):
    nums = {}
    answer = []
    for i in lst:
        nums[str(i)[0]] = i
    compare = list(nums.keys())
    s_compare = sorted(compare, reverse=True)
    for j in s_compare:
        answer.append(str(nums.get(j)))

    return (''.join(answer))
```

결과: 정확성 0.0 = **실패**<br/>
딕셔너리의 key는 중복 될 수 없다.

<h3>두번째 풀이</h3>

```python
def solution(lst):
    nums=[]
    for i in lst:
        nums.append((i%10, i))
    sorted_nums = sorted(nums, key=lambda x : x[0], reverse=True)
    answer = []
    for j in sorted_nums:
        answer.append(str(j[1]))

    return (''.join(answer))
```

결과: 정확성 0.0 = **실패**<br/>
세자리수에 적용되지 않을 뿐더러,, 이 접근법의 개선방법은 떠오르지않는다.

<h3>세번째 풀이</h3>

```python
def solution(lst):
    nums=[]
    for i in lst:
        nums.append(str(i))
    new_nums = []
    for j in nums:
        idx = 0
        while len(j) < 4:
            j += j[idx]
            idx += 1
            if len(j) == 4:
                new_nums.append(j)
    t = []
    for k in range(len(lst)):
        t.append((lst[k], new_nums[k]))
    sorted_nums = sorted(t, key=lambda x : x[1], reverse=True)
    answer = []
    for i in sorted_nums:
        answer.append(str(i[0]))

    return (''.join(answer))
```

결과: 정확성 36.4 = **실패**<br/>
작동은 되는 것 같으나.. 런타임에러

<h3>네번째 풀이</h3>

1. 인풋 리스트(lst) 요소들의 인덱스와 기존의 요소들을 3번 이어붙인 요소로 튜플을 만든 후, 새로운 리스트(num_lst)에 넣어줍니다.
2. 3번 이어붙인 요소들을 기준으로 정렬해줍니다.
3. 해당 요소들의 인덱스에 따라 원래 인풋 리스트의 값을 가져와서 빈 문자열(answer)에 더해줍니다.
4. '00'은 '0'으로 만들어줘야하기 때문에, int로 변환 후 str로 다시 변환해서 리턴합니다. 

```python
def solution(lst):
    answer = ''
    num_lst=[]
    for idx, num in enumerate(lst):
        num_lst.append((idx, str(num)*3))
    num_lst.sort(key=lambda x : x[1], reverse=True)
    for idx, num in num_lst:
        answer += str(lst[idx])
        
    return str(int(answer))
```

<h3>🔶다른 사람의 풀이</h3>

```python
def solution(numbers):
    numbers = list(map(str, numbers))
    numbers.sort(key=lambda x: x*3, reverse=True)
    return str(int(''.join(numbers)))
```
