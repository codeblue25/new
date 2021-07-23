---
layout: post
title: "[프로그래머스 / Python] Level 2 다리를 지나는 트럭"
date: 2021-07-23T15:25:52-05:00
author: codeblue25
categories: Algorithm
---

<h2>문제</h2>

트럭 여러 대가 강을 가로지르는 일차선 다리를 정해진 순으로 건너려 합니다. 모든 트럭이 다리를 건너려면 최소 몇 초가 걸리는지 알아내야 합니다. 다리에는 트럭이 최대 bridge_length대 올라갈 수 있으며, 다리는 weight 이하까지의 무게를 견딜 수 있습니다. 단, 다리에 완전히 오르지 않은 트럭의 무게는 무시합니다. <br />

solution 함수의 매개변수로 다리에 올라갈 수 있는 트럭 수 bridge_length, 다리가 견딜 수 있는 무게 weight, 트럭 별 무게 truck_weights가 주어집니다. 이때 모든 트럭이 다리를 건너려면 최소 몇 초가 걸리는지 return 하도록 solution 함수를 완성하세요.

<h2>제한사항</h2>

- bridge_length는 1 이상 10,000 이하입니다.
- weight는 1 이상 10,000 이하입니다.
- truck_weights의 길이는 1 이상 10,000 이하입니다.
- 모든 트럭의 무게는 1 이상 weight 이하입니다.

<h3>🔹나의 풀이</h3>

```python
def solution(bridge_length, weight, truck_weights):
    count = 0
    bridge = [0] * bridge_length
    while len(truck_weights) > 0:
        count += 1
        bridge.pop(0)
        if sum(bridge) + truck_weights[0] <= weight:
            bridge.append(truck_weights[0])
            truck_weights.pop(0)
        else:
            bridge.append(0)
    return (count + bridge_length)
```
