# 전화번호 목록

[Programmers 42840 문제](https://programmers.co.kr/learn/courses/30/lessons/42840)  

> 완전탐색 문제로 정답개수를 비교하여 가장 큰 사람을 추출하는 문제입니다.

## 메모 할 사항

특별한 문제가 없었습니다. 너무 단순계산이라 더 간단한 방법이 있는지 찾아보았습니다.

## 입출력 예시

answers | return
|---|---|---|
[1,2,3,4,5] | [1]
[1,3,2,4,2] | [1,2,3]

## Result Code

```cpp
#include <string>
#include <vector>
#include <algorithm>

using namespace std;
int SetTest(vector<int> &answer, vector<int> &person);

vector<int> solution(vector<int> answers) {
    vector<int> answer;
    vector<int> collection;
    vector<int> person1, person2, person3;
    person1.push_back(1);
    person1.push_back(2);
    person1.push_back(3);
    person1.push_back(4);
    person1.push_back(5);
    
    person2.push_back(2);
    person2.push_back(1);
    person2.push_back(2);
    person2.push_back(3);
    person2.push_back(2);
    person2.push_back(4);
    person2.push_back(2);
    person2.push_back(5);
    
    person3.push_back(3);
    person3.push_back(3);
    person3.push_back(1);
    person3.push_back(1);
    person3.push_back(2);
    person3.push_back(2);
    person3.push_back(4);
    person3.push_back(4);
    person3.push_back(5);
    person3.push_back(5);

    collection.push_back(SetTest(answers, person1));
    collection.push_back(SetTest(answers, person2));
    collection.push_back(SetTest(answers, person3));
    
    int max = *max_element(collection.begin(), collection.end());
    for( int i = 0; i < collection.size(); i++)
    {
        if ( max == collection[i])
            answer.push_back(i+1);
    }
    
    return answer;
}

int SetTest(vector<int> &answers, vector<int> &person)
{
    int correction = 0;
    for ( int i = 0; i < answers.size(); i++)
    {
        int index = i % person.size();
        
        if ( answers[i] == person[index] )
            correction++;
    }
    
    return correction;
}
```

## 초기테스트

```text
정확성  테스트
테스트 1 〉 통과 (0.01ms, 3.93MB)
테스트 2 〉 통과 (0.01ms, 3.77MB)
테스트 3 〉 통과 (0.01ms, 3.96MB)
테스트 4 〉 통과 (0.03ms, 3.84MB)
테스트 5 〉 통과 (0.01ms, 3.96MB)
테스트 6 〉 통과 (0.01ms, 3.85MB)
테스트 7 〉 통과 (0.10ms, 3.95MB)
테스트 8 〉 통과 (0.03ms, 3.94MB)
테스트 9 〉 통과 (0.17ms, 3.94MB)
테스트 10 〉통과 (0.08ms, 3.93MB)
테스트 11 〉통과 (0.17ms, 3.96MB)
테스트 12 〉통과 (0.16ms, 3.89MB)
테스트 13 〉통과 (0.02ms, 3.95MB)
테스트 14 〉통과 (0.23ms, 3.97MB)
채점 결과
정확성: 100.0
합계: 100.0 / 100.0
```
