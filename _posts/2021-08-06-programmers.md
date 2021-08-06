---
layout: post
title: "[프로그래머스 / Python] Level 1 모의고사"
date: 2021-08-06T15:25:52-05:00
author: codeblue25
categories: Algorithm
---

<h2>문제</h2>

수포자는 수학을 포기한 사람의 준말입니다. 수포자 삼인방은 모의고사에 수학 문제를 전부 찍으려 합니다. 수포자는 1번 문제부터 마지막 문제까지 다음과 같이 찍습니다. <br />
1번 수포자가 찍는 방식: 1, 2, 3, 4, 5, 1, 2, 3, 4, 5, ...<br />
2번 수포자가 찍는 방식: 2, 1, 2, 3, 2, 4, 2, 5, 2, 1, 2, 3, 2, 4, 2, 5, ...<br />
3번 수포자가 찍는 방식: 3, 3, 1, 1, 2, 2, 4, 4, 5, 5, 3, 3, 1, 1, 2, 2, 4, 4, 5, 5, ...<br />
1번 문제부터 마지막 문제까지의 정답이 순서대로 들은 배열 answers가 주어졌을 때, 가장 많은 문제를 맞힌 사람이 누구인지 배열에 담아 return 하도록 solution 함수를 작성해주세요.

<h2>제한사항</h2>

- 시험은 최대 10,000 문제로 구성되어있습니다.
- 문제의 정답은 1, 2, 3, 4, 5중 하나입니다.
- 가장 높은 점수를 받은 사람이 여럿일 경우, return하는 값을 오름차순 정렬해주세요.

<h3>🔹나의 풀이</h3>

```python
def solution(answers):
    person1= [1, 2, 3, 4, 5]
    person2= [2, 1, 2, 3, 2, 4, 2, 5]
    person3= [3, 3, 1, 1, 2, 2, 4, 4, 5, 5]

    score = [0, 0, 0]

    for idx, answer in enumerate(answers):
        if answer == person1[idx%len(person1)]:
            score[0] += 1
        if answer == person2[idx%len(person2)]:
            score[1] += 1
        if answer == person3[idx%len(person3)]:
            score[2] += 1

    answer = []
    for person, total in enumerate(score):
        if total == max(score):
            answer.append(person+1)

    return answer
```

`enumerate()` 함수를 알았기에 어렵지 않게 접근하고 코드를 짤 수 있었다 ^___^ !!ㅋ