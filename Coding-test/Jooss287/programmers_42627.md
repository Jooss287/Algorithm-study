# 디스크 컨트롤러

[Programmers 42627 문제](https://programmers.co.kr/learn/courses/30/lessons/42627)  

> Hash 문제로, 디스크들의 처리순서를 정해 가장 낮은 평균 처리 시간을 구하는 문제입니다.

## 메모 할 사항

set을 사용하여 정렬 기능을 이용하여 처리하고자 하였으나 우선순위 큐로 도중 변경하여 풀이하였습니다.

## 입출력 예시

jobs | return
|---|---|
[[0,3], [1,9], [2,6]] | 9

## Result Code

```cpp
struct customPair {
    int orderTime;
    int tactTime;
    int startTime = 0;
    customPair(pair<int, int> _pair, int time) : orderTime(_pair.first), tactTime(_pair.second), startTime(time) {};
    
    bool operator<(const customPair &rhs) const {
        if ( tactTime > rhs.tactTime )
            return true;
        else
            return false;
    }

    int getTact() const {
        return startTime - orderTime + tactTime;
    }
};

bool isOrderedValue(int endOfTime, set<pair<int,int>>::iterator nextTarget)
{
    return nextTarget->first <= endOfTime;
}

int solution(vector<vector<int>> jobs) {
    int answer = 0;
    int sum = 0;
    int processCnt = 0;
    set<pair<int,int>> orders;
    priority_queue<customPair> q;

    for ( auto& job : jobs)
    {
        orders.insert(make_pair(job[0], job[1]));
    }
    
    auto itr = orders.begin();
    auto nextItr = (orders.begin())++;
    int endOfTime = itr->first;
    
    while(processCnt != orders.size())
    {
        if ( q.empty() )
        {
            sum += itr->second;
            endOfTime = endOfTime + itr->second;
            processCnt++;
            itr++;
        }
        else
        {
            int tact = q.top().getTact();
            sum += tact;
            processCnt++;
            endOfTime = endOfTime + q.top().tactTime;
            q.pop();
            
            int qSize = q.size();
            for ( int i = 0; i < qSize; i++)
            {
                customPair temp(make_pair(q.top().orderTime, q.top().tactTime), endOfTime);
                q.pop();
                q.push(temp);
            }
        }

        while ( itr != orders.end() && isOrderedValue(endOfTime, itr) )
        {
            q.push(customPair(*itr, endOfTime));
            itr++;
        }
    }
    
    return ceil(sum / processCnt);
}
```

### Result Code 테스트 결과

```text
정확성  테스트
테스트 1 〉통과 (54.68ms, 4.27MB)
테스트 2 〉통과 (49.41ms, 4.33MB)
테스트 3 〉통과 (0.06ms, 4.2MB)
테스트 4 〉통과 (0.13ms, 3.66MB)
테스트 5 〉통과 (1.13ms, 4.27MB)
테스트 6 〉통과 (0.14ms, 4.32MB)
테스트 7 〉통과 (0.04ms, 3.74MB)
테스트 8 〉통과 (0.26ms, 4.33MB)
```

## 초기 작성한 코드

```cpp
struct customPair {
    int orderTime;
    int tactTime;
    int startTime = 0;
    customPair(pair<int, int> _pair, int time) : orderTime(_pair.first), tactTime(_pair.second), startTime(time) {};
    
    bool operator<(const customPair &rhs) const {
        if ( getTact() > rhs.getTact() )
            return true;
        else
            return false;
    }

    int getTact() const {
        return startTime - orderTime + tactTime;
    }
};

bool isOrderedValue(int endOfTime, set<pair<int,int>>::iterator nextTarget)
{
    return nextTarget->first <= endOfTime;
}

int solution(vector<vector<int>> jobs) {
    int answer = 0;
    int sum = 0;
    int processCnt = 0;
    set<pair<int,int>> orders;
    priority_queue<customPair> q;

    for ( auto& job : jobs)
    {
        orders.insert(make_pair(job[0], job[1]));
    }
    
    auto itr = orders.begin();
    auto nextItr = (orders.begin())++;
    int endOfTime = itr->first;
    
    while(processCnt != orders.size())
    {
        if ( q.empty() )
        {
            sum += itr->second;
            endOfTime = endOfTime + itr->second;
            processCnt++;
            itr++;
        }
        else
        {
            int tact = q.top().getTact();
            sum += tact;
            processCnt++;
            endOfTime = endOfTime + q.top().tactTime;
            q.pop();
            
            int qSize = q.size();
            for ( int i = 0; i < qSize; i++)
            {
                customPair temp(make_pair(q.top().orderTime, q.top().tactTime), endOfTime);
                q.pop();
                q.push(temp);
            }
        }

        while ( itr != orders.end() && isOrderedValue(endOfTime, itr) )
        {
            q.push(customPair(*itr, endOfTime));
            itr++;
        }
    }
    
    return ceil(sum / processCnt);
}
```

### 초기테스트

```text
정확성  테스트
테스트 1 〉실패 (4.83ms, 4.27MB)
테스트 2 〉실패 (5.25ms, 4.27MB)
테스트 3 〉실패 (3.15ms, 4.26MB)
테스트 4 〉실패 (2.42ms, 4.33MB)
테스트 5 〉실패 (4.20ms, 4.27MB)
테스트 6 〉실패 (0.02ms, 4.33MB)
테스트 7 〉실패 (1.94ms, 4.2MB)
테스트 8 〉실패 (1.28ms, 3.66MB)
테스트 9 〉실패 (0.19ms, 4.27MB)
테스트 10 〉실패 (5.07ms, 3.79MB)
테스트 11 〉실패 (0.01ms, 4.34MB)
테스트 12 〉실패 (0.01ms, 4.32MB)
테스트 13 〉실패 (0.01ms, 3.69MB)
테스트 14 〉통과 (0.01ms, 4.33MB)
테스트 15 〉통과 (0.01ms, 4.27MB)
테스트 16 〉통과 (0.01ms, 4.33MB)
테스트 17 〉통과 (0.01ms, 4.27MB)
테스트 18 〉통과 (0.01ms, 4.33MB)
테스트 19 〉통과 (0.01ms, 4.33MB)
테스트 20 〉통과 (0.01ms, 4.33MB)
```
