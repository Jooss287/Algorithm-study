# 섬 연결하기

[Programmers 42861 문제](https://programmers.co.kr/learn/courses/30/lessons/42861)  

> 탐욕법(Greedy)문제로, 여러 섬들을 연결하는 최소 cost의 다리를 생성하는 문제입니다.

## 메모 할 사항

하나의 섬에서 가장 cost가 낮은 다리를 선택하여 다리를 연결하고, 연결된 섬을 하나로 판단하여 문제를 풀었습니다.
multimap을 사용하여 다리의 cost를 나타내었으나, class를 이용하였으면 조금 더 깔끔한 풀이가 될 수 있을거라 생각합니다.

## 입출력 예시

numbers | target | return
|---|---|---|
[1, 1, 1, 1, 1] | 3 | 5

## Result Code

```cpp
multimap<int, int>::iterator findLowCost(multimap<int, int> &targetCost) {
    int lowCost = targetCost.begin()->second;
    multimap<int, int>::iterator ret = targetCost.begin();

    for ( auto itr = targetCost.begin(); itr != targetCost.end(); itr++ )
    {
        if ( itr->second < lowCost )
        {
            lowCost = itr->second;
            ret = itr;
        }
    }
    return ret;
}

void connectIsland(multimap<int, multimap<int, int>> &islandInfo, int islandNumber1, int islandNumber2, set<int> &mergedIsland ) {
    auto islandInfo1 = islandInfo.find(islandNumber1);
    auto islandInfo2 = islandInfo.find(islandNumber2);

    islandInfo1->second.insert(islandInfo2->second.begin(), islandInfo2->second.end());

    mergedIsland.insert(islandNumber2);
    for ( auto number : mergedIsland )
        islandInfo1->second.erase(number);

    islandInfo.erase(islandNumber2);
}

int solution(int n, vector<vector<int>> costs) {
    int answer = 0;
    // [0]과 [1] 다리를 연결하는데 소비 cost [2]
    multimap<int, multimap<int, int>> islandInfo;       // [0], <[1],[2]>
    
    for(int i = 0; i < static_cast<int>(costs.size()); i++)
    {
        auto costInfo = costs[i];
        auto targetIsland = islandInfo.find(costInfo[0]);
        if ( targetIsland == islandInfo.end())
        {
            multimap<int,int> temp1{make_pair(costInfo[1], costInfo[2])};
            islandInfo.insert(make_pair(costInfo[0], temp1));
        }
        else
        {
            targetIsland->second.insert(make_pair(costInfo[1], costInfo[2]));
        }

        targetIsland = islandInfo.find(costInfo[1]);
        if ( targetIsland == islandInfo.end())
        {
            multimap<int,int> temp1{make_pair(costInfo[0], costInfo[2])};
            islandInfo.insert(make_pair(costInfo[1], temp1));
        }
        else
        {
            targetIsland->second.insert(make_pair(costInfo[0], costInfo[2]));
        }
    }

    auto itr = islandInfo.begin();
    set<int> mergedIsland;
    mergedIsland.insert(0);
    while(islandInfo.size() != 1)
    {
        auto lowCostBridge = findLowCost(itr->second);
        answer += lowCostBridge->second;
        connectIsland(islandInfo, itr->first, lowCostBridge->first, mergedIsland);
        
    }
    return answer;
}
```

### Result Code 테스트 결과

```text
정확성  테스트
테스트 1 〉통과 (0.01ms, 4.32MB)
테스트 2 〉통과 (0.02ms, 4.27MB)
테스트 3 〉통과 (0.03ms, 4.34MB)
테스트 4 〉통과 (0.04ms, 4.27MB)
테스트 5 〉통과 (0.03ms, 4.27MB)
테스트 6 〉통과 (0.06ms, 4.32MB)
테스트 7 〉통과 (0.06ms, 4.33MB)
테스트 8 〉통과 (0.02ms, 4.28MB)
```

## 초기 작성한 코드

```cpp

```

### 초기테스트

```text
```
