# 더 맵게

[Programmers 42626 문제](https://programmers.co.kr/learn/courses/30/lessons/42626)  

> Heap 스코빌 지수가 가장 낮은 두가지를 섞어서 모든 음식이 일정 스코빌 이상의 음식이 되도록 만드는 문제입니다.

## 메모 할 사항

set을 이용해서 자동으로 정렬하도록 한 뒤 iterator을 이용하여 첫번째, 두번째 값을 계속 섞도록 했습니다. 가장 낮은값이 K보다 클 경우 까지의 횟수가 섞은 횟수입니다.

* Priority_Queue의 존재를 알아야 합니다.
* 우선순위 큐의 정렬 기준 Constructor을 알아야 합니다.

## 입출력 예시

scoville | k | return
|---|---|---|
[1,2,3,9,10,12] | 7 | 2 |

## Result Code

```cpp
#include <string>
#include <vector>
#include <set>
#include <queue>
#include <iostream>

using namespace std;

int shakeScoville(const int &smallest, const int &largest)
{
    return smallest + (largest * 2);
}

int solution(vector<int> scoville, int K) {
    int answer = 0;
    priority_queue<int, vector<int>, greater<int>> scovilleQueue;
    set<int> orderedScoville;
    
    for(auto& level : scoville)
        scovilleQueue.push(level);
    
    while( scovilleQueue.size() > 1 )
    {
        if ( scovilleQueue.top() >= K)
            break;
        
        auto itr = orderedScoville.begin();
        int smallestScoville = scovilleQueue.top();
        scovilleQueue.pop();
        int nextScoville = scovilleQueue.top();
        scovilleQueue.pop();
        
        int shakedScoville = shakeScoville(smallestScoville, nextScoville);
        scovilleQueue.push(shakedScoville);
        
        answer++;
    }
    
    if ( (scovilleQueue.size() == 1) && (scovilleQueue.top() < K) )
        answer = -1;
    
    return answer;
}
```

### Result Code 테스트 결과

```text
정확성  테스트
테스트 1 〉 통과 (0.01ms, 4.33MB)
테스트 2 〉 통과 (0.01ms, 4.32MB)
테스트 3 〉 통과 (0.01ms, 4.34MB)
테스트 4 〉 통과 (0.01ms, 3.63MB)
테스트 5 〉 통과 (0.01ms, 4.33MB)
테스트 6 〉 통과 (0.07ms, 4.27MB)
테스트 7 〉 통과 (0.07ms, 4.26MB)
테스트 8 〉 통과 (0.01ms, 4.31MB)
테스트 9 〉 통과 (0.01ms, 4.26MB)
테스트 10 〉통과 (0.05ms, 4.27MB)
테스트 11 〉통과 (0.04ms, 4.27MB)
테스트 12 〉통과 (0.11ms, 4.21MB)
테스트 13 〉통과 (0.06ms, 4.34MB)
테스트 14 〉통과 (0.01ms, 3.75MB)
테스트 15 〉통과 (0.09ms, 4.27MB)
테스트 16 〉통과 (0.01ms, 4.21MB)
효율성  테스트
테스트 1 〉통과 (26.92ms, 9.27MB)
테스트 2 〉통과 (51.31ms, 14.8MB)
테스트 3 〉통과 (201.50ms, 39.6MB)
테스트 4 〉통과 (21.13ms, 7.95MB)
테스트 5 〉통과 (227.17ms, 41.2MB)
```

## 초기 작성한 코드

```cpp
#include <string>
#include <vector>
#include <set>
#include <iostream>

using namespace std;

int shakeScoville(const int &smallest, const int &largest)
{
    return smallest + (largest * 2);
}

int solution(vector<int> scoville, int K) {
    int answer = 0;
    set<int> orderedScoville;
    
    for(auto& level : scoville)
        orderedScoville.insert(level);
    
    while( orderedScoville.size() > 1 )
    {
        if ( *orderedScoville.begin() >= K)
            break;
        
        auto itr = orderedScoville.begin();
        int smallestScoville = *itr++;
        int nextScoville = *itr;
        int shakedScoville = shakeScoville(smallestScoville, nextScoville);
        orderedScoville.erase(smallestScoville);
        orderedScoville.erase(nextScoville);
        orderedScoville.insert(shakedScoville);
        
        answer++;
    }
    
    if ( (orderedScoville.size() == 1) && (*orderedScoville.begin() < K) )
        answer = -1;
    
    return answer;
}
```

### 초기테스트

```text
정확성  테스트
테스트 1 〉 통과 (0.01ms, 4.27MB)
테스트 2 〉 통과 (0.01ms, 4.32MB)
테스트 3 〉 통과 (0.01ms, 3.66MB)
테스트 4 〉 통과 (0.01ms, 4.2MB)
테스트 5 〉 통과 (0.01ms, 4.2MB)
테스트 6 〉 통과 (0.18ms, 4.33MB)
테스트 7 〉 통과 (0.15ms, 3.71MB)
테스트 8 〉 통과 (0.03ms, 3.61MB)
테스트 9 〉 통과 (0.04ms, 4.32MB)
테스트 10 〉 통과 (0.12ms, 4.21MB)
테스트 11 〉 통과 (0.08ms, 4.27MB)
테스트 12 〉 실패 (0.36ms, 4.32MB)
테스트 13 〉 통과 (0.15ms, 4.25MB)
테스트 14 〉 통과 (0.01ms, 3.66MB)
테스트 15 〉 통과 (0.19ms, 4.2MB)
테스트 16 〉 통과 (0.01ms, 3.7MB)
효율성  테스트
테스트 1 〉 실패 (70.93ms, 14.5MB)
테스트 2 〉 실패 (134.80ms, 23.7MB)
테스트 3 〉 실패 (641.95ms, 63.1MB)
테스트 4 〉 실패 (55.12ms, 12.4MB)
테스트 5 〉 실패 (643.94ms, 65.6MB)
```
