# 위장

[Programmers 42578 문제](https://programmers.co.kr/learn/courses/30/lessons/42578)  

> Hash 문제로 의상들을 조합하여 의상 조합의 경우의 수를 구하는 문제입니다.

## 메모 할 사항

의상들의 조합을 구하기 위해 각 의상 부위별로 Map을 이용하여 정리합니다. 각 부위별로 안 입는 경우의 수를 추가하여 경우의 수를 구합니다.
하나도 안 입는 경우의 수를 제외하기 위하여 총 경우의 수에서 1을 빼어서 값을 도출했습니다.

## 입출력 예시

number | k | return
|---|---|---|
"1294" | 2 | "94"
"1231234" | 3 | "3234"
"4177252841" | 4 | "775841"

## Result Code

```cpp
#include <string>
#include <vector>
#include <map>

using namespace std;

int solution(vector<vector<string>> clothes) {
    int answer = 1;
    map<string, vector<string>> item_map;
    
    for (auto& item : clothes)
    {
        if (item_map.find(item[1]) == item_map.end())
            item_map.insert(make_pair(item[1], vector<string>()));
        item_map[item[1]].push_back(item[0]);
    }
    for (auto& keyValuePair : item_map)
    {
        keyValuePair.second.push_back(string());
        answer *= keyValuePair.second.size();
    }
    
    return answer-1;
}
```

### Result Code 테스트 결과

```text
테스트 1 〉 통과 (0.02ms, 3.75MB)
테스트 2 〉 통과 (0.02ms, 3.99MB)
테스트 3 〉 통과 (0.02ms, 3.96MB)
테스트 4 〉 통과 (0.03ms, 3.99MB)
테스트 5 〉 통과 (0.02ms, 3.98MB)
테스트 6 〉 통과 (0.02ms, 3.69MB)
테스트 7 〉 통과 (0.04ms, 4.39MB)
테스트 8 〉 통과 (0.02ms, 3.99MB)
테스트 9 〉 통과 (0.01ms, 3.69MB)
테스트 10 〉 통과 (0.02ms, 3.75MB)
테스트 11 〉 통과 (0.01ms, 3.75MB)
테스트 12 〉 통과 (0.04ms, 4.34MB)
테스트 13 〉 통과 (0.03ms, 3.96MB)
테스트 14 〉 통과 (0.01ms, 3.96MB)
테스트 15 〉 통과 (0.01ms, 3.77MB)
테스트 16 〉 통과 (0.01ms, 4.34MB)
테스트 17 〉 통과 (0.02ms, 4.34MB)
테스트 18 〉 통과 (0.02ms, 3.75MB)
테스트 19 〉 통과 (0.03ms, 3.75MB)
테스트 20 〉 통과 (0.02ms, 3.92MB)
테스트 21 〉 통과 (0.02ms, 3.75MB)
테스트 22 〉 통과 (0.01ms, 3.99MB)
테스트 23 〉 통과 (0.01ms, 3.75MB)
테스트 24 〉 통과 (0.02ms, 4.34MB)
테스트 25 〉 통과 (0.03ms, 3.93MB)
테스트 26 〉 통과 (0.03ms, 3.92MB)
테스트 27 〉 통과 (0.01ms, 4.29MB)
테스트 28 〉 통과 (0.02ms, 3.76MB)
```

## 초기 작성한 코드

```cpp

```

### 초기테스트

```text
```
