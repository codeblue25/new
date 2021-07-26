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

0. 트럭의 움직임에 따라 0을 추가하고 삭제하는 방식을 채택합니다.
1. bridge_length만큼 0으로 구성된 bridge 리스트를 생성합니다.
2. while문이 시작되면, 트럭의 움직임이 있다는 것을 의미합니다. 따라서 일단 count에 1을 더해줌과 동시에 bridge 리스트의 첫번째 원소를 삭제합니다.
3. 다리 위에 있는 트럭 + 기다리는 다음 트럭의 합과 weight를 비교합니다.
4. 다음 트럭이 다리에 올라갈 수 있으면 트럭을 추가해주고, 올라갈 수 없다면 0을 추가해서 트럭을 앞으로 당깁니다.
5. 마지막 트럭은 기다리는 트럭이 없음으로, 다리를 나가기 위해 bridge_length 만큼 더하여 count를 리턴합니다.

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

<h3>🔶다른 사람의 풀이</h3>

```python
import collections

DUMMY_TRUCK = 0


class Bridge(object):

    def __init__(self, length, weight):
        self._max_length = length
        self._max_weight = weight
        self._queue = collections.deque()
        self._current_weight = 0

    def push(self, truck):
        next_weight = self._current_weight + truck
        if next_weight <= self._max_weight and len(self._queue) < self._max_length:
            self._queue.append(truck)
            self._current_weight = next_weight
            return True
        else:
            return False

    def pop(self):
        item = self._queue.popleft()
        self._current_weight -= item
        return item

    def __len__(self):
        return len(self._queue)

    def __repr__(self):
        return 'Bridge({}/{} : [{}])'.format(self._current_weight, self._max_weight, list(self._queue))


def solution(bridge_length, weight, truck_weights):
    bridge = Bridge(bridge_length, weight)
    trucks = collections.deque(w for w in truck_weights)

    for _ in range(bridge_length):
        bridge.push(DUMMY_TRUCK)

    count = 0
    while trucks:
        bridge.pop()

        if bridge.push(trucks[0]):
            trucks.popleft()
        else:
            bridge.push(DUMMY_TRUCK)

        count += 1

    while bridge:
        bridge.pop()
        count += 1

    return count


def main():
    print(solution(2, 10, [7, 4, 5, 6]), 8)
    print(solution(100, 100, [10]), 101)
    print(solution(100, 100, [10, 10, 10, 10, 10, 10, 10, 10, 10, 10]), 110)


if __name__ == '__main__':
    main()
```

_나두 클래스로 코드 짜는 거.. 알고리즘 수업때 배우고 있지만, 아직도 넘 어렵다🙄_
