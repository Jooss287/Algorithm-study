# 단속카메라

[Programmers 42884 문제](https://programmers.co.kr/learn/courses/30/lessons/42884)  

> Greedy 문제로, 고속도로를 지나는 모든 차량이 한번은 단속카메라를 만나게 할 때, 가장 작은 카메라 개수를 구하는 문제입니다.

## 메모 할 사항

고속도로의 시작과 끝 지점을 pair type을 이용해서 표현했습니다.
모든 고속도로를 set을 이용하여 정렬(pair는 first -> second 순으로 오름차순정렬)하고 제일 앞 고속도로부터 계산했습니다.
첫 pair 내에서 겹치는 고속도로들을 모아 카메라 하나를 설치합니다.
남은 pair들중 시작지점이 낮은 값을 가지는 고속도로를 기준으로 겹치는 고속도로를 모아 또 하나의 카메라를 설치합니다.
모든 고속도로에 카메라가 설치될때까지 반복합니다.

처음 겹치는 구간이 곧 고속도로 카메라를 놓는 위치라고 가정하여 반복하는 문제로 풀었습니다.

## 입출력 예시

routes | return
|---|---|
[[-20,15], [-14,-5], [-18,-13], [-5,-3]] | 2

## Result Code

```cpp
struct RoutePair {
    int cameraIndex;
    pair<int, int> routePair;
    RoutePair(int index, int start, int end) : cameraIndex(index), routePair(make_pair(start, end)) {};
    bool isInclude(int position) const {
        if ( ( position >= routePair.first ) && ( position <= routePair.second))
            return true;
        return false;
    }

    bool operator<(const RoutePair& rhs) const {
        return routePair < rhs.routePair;
    }
};

int solution(vector<vector<int>> routes) {
    int answer = 0;
    set<int> meetCamera;
    set<RoutePair> routePair;
    
    for ( int i = 0; i < static_cast<int>(routes.size()); ++i)
    {
        routePair.insert(RoutePair(i, routes[i][0], routes[i][1]));
    }
    
    set<RoutePair>::iterator itr = routePair.begin();
    set<RoutePair>::iterator targetItr = ++(routePair.begin());
    int startPoint = itr->routePair.first;
    while(meetCamera.size() != routePair.size())
    {
        meetCamera.insert(itr->cameraIndex);
        pair<int, int> groupRange = make_pair(itr->routePair.first, itr->routePair.second);
        while( (targetItr->routePair.first >= groupRange.first ) && (targetItr->routePair.first <= groupRange.second) )
        {
            meetCamera.insert(targetItr->cameraIndex);

            groupRange.first = targetItr->routePair.first;
            if ( targetItr->routePair.second < groupRange.second)
                groupRange.second = targetItr->routePair.second;
            targetItr++;
        }
        answer++;
        itr = targetItr;
        targetItr++;
    }

    return answer;
}
```

### Result Code 테스트 결과

```text
정확성  테스트
테스트 1 〉통과 (0.02ms, 3.69MB)
테스트 2 〉통과 (0.03ms, 4.32MB)
테스트 3 〉통과 (0.04ms, 3.75MB)
테스트 4 〉통과 (0.04ms, 3.76MB)
테스트 5 〉통과 (0.04ms, 4.31MB)
효율성  테스트
테스트 1 〉통과 (0.68ms, 4.14MB)
테스트 2 〉통과 (0.37ms, 3.93MB)
테스트 3 〉통과 (1.33ms, 4.11MB)
테스트 4 〉통과 (0.07ms, 3.91MB)
테스트 5 〉통과 (1.80ms, 4.35MB)
```

## 초기 작성한 코드

```cpp

```

### 초기테스트

```text
```
