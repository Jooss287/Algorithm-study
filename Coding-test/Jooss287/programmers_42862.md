# 소수 찾기

[Programmers 42862 문제](https://programmers.co.kr/learn/courses/30/lessons/42862)  

> 탐욕법(Greed) 문제로 체육복을 나눠 주어 최대한 많은 사람이 수업을 들을 수 있도록 하는 문제입니다.

## 메모 할 사항

바로 앞사람이나 뒷사람에게 체육복을 나누어 주려면 모든 학생들을 Vector로 보유상황을 나열하고 앞, 뒤부터 차례대로 문제를 해결 해 봅니다.

* 주어진 조건의 배열이 정렬이 되어 있다는 보장을 하지 못합니다. 정렬을 항시 신경써야 합니다.
* Lost - Reserve 둘다 적용되는 사람이 있다면 Reserve를 사용해서 주위에 체육복을 나누어 줄 때 자기 값이 2여야만 나누어 줄 수 있습니다. 이 조건을 해결했더니 전부 해결가능했습니다.

## 입출력 예시

n | lost | reserve | return
|---|---|---|---|
5 | [2,4] | [1,3,5] | 5
5 | [2,4] | [3] | 4
3 | [3] | [1] | 2

## Result Code

```cpp
#include <string>
#include <vector>
#include <algorithm>
#include <iostream>

using namespace std;

int solution(int n, vector<int> lost, vector<int> reserve) {
    int answer = 0;
    sort(lost.begin(), lost.end());
    sort(reserve.begin(), reserve.end());

    vector<int> student(n, 1);
    for(int lostStudent : lost)
        student[lostStudent-1] -= 1;
    for(int reserveStudent : reserve)
        student[reserveStudent-1] += 1;
    
    for (int stu : student)
        cout << stu << " ";
    cout << endl;
    
    for(int reserveStudent : reserve)
    {
        const int preNumStudent = reserveStudent - 2;
        const int myNumStudent = reserveStudent - 1;
        const int nextNumStudent = reserveStudent;
        
        if (student[myNumStudent] != 2)
            continue;
        if ( ( preNumStudent >= 0) && ( student[preNumStudent] == 0) )
        {
            student[preNumStudent] = 1;
            student[myNumStudent] = 1;
            continue;
        }
        if ( ( nextNumStudent < n) && ( student[nextNumStudent] == 0) )
        {
            student[nextNumStudent] = 1;
            student[myNumStudent] = 1;
            continue;
        }
    }
    
    for(int& haveSuit : student)
    {
        if(haveSuit >= 1)
            answer++;
        cout << haveSuit << " ";
    }
        
    return answer;
}
```

## 초기 작성한 코드

```cpp
#include <string>
#include <vector>
#include <algorithm>
#include <iostream>

using namespace std;

int solution(int n, vector<int> lost, vector<int> reserve) {
    int answer = 0;
    sort(lost.begin(), lost.end());
    sort(reserve.begin(), reserve.end());

    vector<int> student(n, 1);
    for(int lostStudent : lost)
        student[lostStudent-1] -= 1;
    for(int reserveStudent : reserve)
        student[reserveStudent-1] += 1;
    
    for(int reserveStudent : reserve)
    {
        const int preNumStudent = reserveStudent - 2;
        const int myNumStudent = reserveStudent - 1;
        const int nextNumStudent = reserveStudent;
        if ( ( preNumStudent >= 0) && ( student[preNumStudent] == 0) )
        {
            student[preNumStudent] = 1;
            student[myNumStudent] = 1;
            continue;
        }
        if ( ( nextNumStudent < n) && ( student[nextNumStudent] == 0) )
        {
            student[nextNumStudent] = 1;
            student[myNumStudent] = 1;
            continue;
        }
    }
    
    for(int& haveSuit : student)
    {
        if(haveSuit >= 1)
            answer++;
        cout << haveSuit << " ";
    }
        
    return answer;
}
}
```

### 초기테스트

```text
테스트 1 〉 실패 (0.02ms, 3.74MB)
테스트 2 〉 실패 (0.02ms, 3.98MB)
테스트 3 〉 실패 (0.02ms, 4.32MB)
테스트 4 〉 통과 (0.02ms, 3.74MB)
테스트 5 〉 실패 (0.02ms, 3.59MB)
테스트 6 〉 실패 (0.02ms, 3.98MB)
테스트 7 〉 통과 (0.03ms, 4.34MB)
테스트 8 〉 통과 (0.02ms, 3.97MB)
테스트 9 〉 실패 (0.03ms, 3.75MB)
테스트 10 〉실패 (0.02ms, 3.98MB)
테스트 11 〉통과 (0.02ms, 3.73MB)
테스트 12 〉실패 (0.02ms, 3.68MB)
테스트 13 〉통과 (0.02ms, 3.98MB)
```
