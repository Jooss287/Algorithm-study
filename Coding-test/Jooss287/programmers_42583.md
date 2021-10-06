# 큰 수 만들기

[Programmers 42883 문제](https://programmers.co.kr/learn/courses/30/lessons/42883)  

> 스택/큐(Stack/Queue)문제로, 다리 위를 지나는 트럭이 모두 지나갈 때의 시간을 구하는 문제입니다.

## 메모 할 사항

구조체를 이용하여 데이터를 저장하고, Queue를 이용해서 다리를 구현하였습니다.

## 입출력 예시

bridge_length | weight | truck_weight | return
|---|---|---|---|
2 | 10 | [7,4,5,6] | 8
100 | 100 | [10] | 101
100 | 100 | [10,10,10,10,10,10,10,10,10,10] | 110

## Result Code

```cpp
struct TRUCK{
    int weight;
    int inputTime;
    TRUCK(int _weight, int _inputTime) : weight(_weight), inputTime(_inputTime) {}
};

int solution(int bridge_length, int weight, vector<int> truck_weights) {
    int answer = 0;
    int truckMoved = 0;
    queue<TRUCK> bridge;
    int startTruckCnt = 0;
    int time = 0;
    int totalWeight = 0;

    while(truckMoved != truck_weights.size())
    {
        time++;

        if ( (!bridge.empty()) && ((time - bridge.front().inputTime) >= bridge_length) )
        {
            truckMoved++;
            totalWeight -= bridge.front().weight;
            bridge.pop();
        }

        if ( totalWeight + truck_weights[startTruckCnt] <= weight)
        {
            TRUCK truck(truck_weights[startTruckCnt], time);
            totalWeight += truck_weights[startTruckCnt];
            startTruckCnt++;
            bridge.push(truck);
        }
        
    }

    return time;
}
```

### Result Code 테스트 결과

```text
정확성  테스트
테스트 1 〉통과 (0.01ms, 4.33MB)
테스트 2 〉통과 (0.11ms, 3.66MB)
테스트 3 〉통과 (0.01ms, 3.74MB)
테스트 4 〉통과 (0.06ms, 4.26MB)
테스트 5 〉통과 (0.47ms, 4.34MB)
테스트 6 〉통과 (0.13ms, 4.26MB)
테스트 7 〉통과 (0.02ms, 4.27MB)
테스트 8 〉통과 (0.01ms, 4.27MB)
테스트 9 〉통과 (0.04ms, 4.27MB)
테스트 10 〉통과 (0.01ms, 4.32MB)
테스트 11 〉통과 (0.01ms, 3.66MB)
테스트 12 〉통과 (0.01ms, 4.33MB)
테스트 13 〉통과 (0.02ms, 4.27MB)
테스트 14 〉통과 (0.01ms, 4.32MB)
```

## 초기 작성한 코드

```cpp

```

### 초기테스트

```text
```
