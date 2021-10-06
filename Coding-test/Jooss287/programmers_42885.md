# 구명보트

[Programmers 42885 문제](https://programmers.co.kr/learn/courses/30/lessons/42885)  

> Greedy 문제로 사람들을 구출하기 위한 최소 구명 보트를 구하는 문제입니다.

## 메모 할 사항

sort를 통하여 몸무게를 정렬하여 앞, 뒤(min, max)의 값을 정리하여 결과를 구하였습니다.
max 값을 통해서 한 명 밖에 못 타는 조건과, 여러명 탈 수 있는 조건을 나누었습니다.

* 초기 조건에서 최대 2명밖에 탈 수 없다는 문제를 확인하지 못하였습니다.
* remove를 안 쓰고 쓸 수 있는 방법을 고민하는 버릇을 들여야 합니다.

## 입출력 예시

people | limit | return
|---|---|---|
[70, 50, 80, 50] | 100 | 3
[70, 80, 50] | 100 | 3

## Result Code

```cpp
inline bool isUnderLimit(const int min, const int max, const int limit) {
    return (min+max) <= limit ? true : false;
}

int solution(vector<int> people, int limit) {
    // 1~50,000명
    // 40kg ~ 240kg 사람무게
    // 40kg ~ 240kg 보트무게
    int answer = 0;

    sort(people.begin(), people.end());
    int min_pointer = 0;
    int max_pointer = people.size()-1;

    while(min_pointer <= max_pointer)
    {
        int maxWeight = people[max_pointer];
        int minWeight = people[min_pointer];
        
        if ( isUnderLimit(minWeight, maxWeight, limit) )
        {
            min_pointer++;
        }
        max_pointer--;
        answer++;
    }
    return answer;
}
```

### Result Code 테스트 결과

```text
정확성  테스트
테스트 1 〉통과 (0.19ms, 4.27MB)
테스트 2 〉통과 (0.11ms, 4.33MB)
테스트 3 〉통과 (0.13ms, 4.27MB)
테스트 4 〉통과 (0.13ms, 4.2MB)
테스트 5 〉통과 (0.08ms, 3.71MB)
테스트 6 〉통과 (0.04ms, 4.32MB)
테스트 7 〉통과 (0.08ms, 3.7MB)
테스트 8 〉통과 (0.01ms, 4.33MB)
테스트 9 〉통과 (0.02ms, 4.32MB)
테스트 10 〉통과 (0.12ms, 4.33MB)
테스트 11 〉통과 (0.11ms, 4.21MB)
테스트 12 〉통과 (0.10ms, 4.27MB)
테스트 13 〉통과 (0.13ms, 4.33MB)
테스트 14 〉통과 (0.13ms, 3.77MB)
테스트 15 〉통과 (0.02ms, 4.25MB)
효율성  테스트
테스트 1 〉통과 (1.97ms, 4.72MB)
테스트 2 〉통과 (1.79ms, 4.78MB)
테스트 3 〉통과 (1.55ms, 4.52MB)
테스트 4 〉통과 (1.51ms, 4.75MB)
테스트 5 〉통과 (1.30ms, 4.39MB)
```

## 초기 작성한 코드

```cpp
inline int getMaxWeight(list<int> &_list) {
    int max = _list.back();
    _list.pop_back();
    return max;
}

inline list<int>::iterator getRemainBiggest(list<int> &_list, const int limit, const int nowWeight) {
    if (_list.empty())
        return _list.end();
    
    list<int>::iterator ret = _list.end();
    ret--;

    for(auto itr = _list.begin(); itr != _list.end(); ++itr)
    {
        int itrValue = *itr;
        if (  (itrValue + nowWeight) > limit)
        {
            if ( itr == _list.begin())
            {
                ret = _list.end();
                break;
            }
            else
                itr--;
            ret = itr;
            break;
        }
    }
    return ret;
}

int solution(vector<int> people, int limit) {
    // 1~50,000명
    // 40kg ~ 240kg 사람무게
    // 40kg ~ 240kg 보트무게
    int answer = 0;

    sort(people.begin(), people.end());
    list<int> peopleList(people.begin(), people.end());
    
    while(!peopleList.empty())
    {
        int maxWeight = getMaxWeight(peopleList);
        int sumWeight = 0;

        if ( maxWeight <= limit / 2.)
        {
            answer += ceil((peopleList.size()+1) / 2.);
            break;
        }
        
        auto remain = getRemainBiggest(peopleList, limit, maxWeight);
        if(remain != peopleList.end())
        {
            sumWeight += *remain;
            peopleList.erase(remain);
        }
        answer++;
    }
    return answer;
}
```

### 초기테스트

```text
정확성  테스트
테스트 1 〉통과 (0.57ms, 4.27MB)
테스트 2 〉통과 (0.25ms, 4.33MB)
테스트 3 〉통과 (0.31ms, 4.33MB)
테스트 4 〉통과 (0.33ms, 4.3MB)
테스트 5 〉통과 (0.20ms, 4.32MB)
테스트 6 〉통과 (0.09ms, 4.27MB)
테스트 7 〉통과 (0.16ms, 4.32MB)
테스트 8 〉통과 (0.02ms, 4.33MB)
테스트 9 〉통과 (0.03ms, 3.69MB)
테스트 10 〉통과 (0.42ms, 4.26MB)
테스트 11 〉통과 (0.25ms, 4.32MB)
테스트 12 〉통과 (0.22ms, 4.33MB)
테스트 13 〉통과 (0.43ms, 4.33MB)
테스트 14 〉통과 (0.28ms, 4.27MB)
테스트 15 〉통과 (0.05ms, 4.21MB)
효율성  테스트
테스트 1 〉통과 (7.63ms, 6.15MB)
테스트 2 〉통과 (4.58ms, 6.19MB)
테스트 3 〉실패 (시간 초과)
테스트 4 〉통과 (3.66ms, 6.34MB)
테스트 5 〉통과 (3.35ms, 5.95MB)
```
