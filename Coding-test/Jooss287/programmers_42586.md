# 소수 찾기

[Programmers 42586 문제](https://programmers.co.kr/learn/courses/30/lessons/42586)  

> Queue 문제로 작업 진도에 따라 한번에 배포되는 기능의 수를 구하는 문제입니다.

## 메모 할 사항

주어진 progresses와 speeds로 각 기능이 구해지는데 걸리는 날짜를 Queue로 구현하였습니다.
Queue에서 front부터 한번에 배포 가능한 기능의 개수를 구하였습니다.

## 입출력 예시

progresses | speeds | return
|---|---|---|
[93, 30, 55] | [1, 30, 5] | [2, 1]
[95, 90, 99, 99, 80, 99] | [1, 1, 1, 1, 1, 1] | [1, 3, 2]

## Result Code

```cpp
vector<int> solution(vector<int> progresses, vector<int> speeds) {
    vector<int> answer;
    queue<int> releaseDay;

    for(int i = 0; i < static_cast<int>(progresses.size()); i++)
    {
        int release = ceil((100 - progresses[i]) / static_cast<double>(speeds[i]));
        releaseDay.push(release);
    }

    while(!releaseDay.empty())
    {
        int releaseCnt = 1;
        int day = releaseDay.front();
        releaseDay.pop();
        while((!releaseDay.empty()) && (releaseDay.front() <= day))
        {
            releaseCnt++;
            releaseDay.pop();
        }
        answer.push_back(releaseCnt);
    }

    return answer;
}
```

### Result Code 테스트 결과

```text
테스트 1 〉통과 (0.01ms, 4.33MB)
테스트 2 〉통과 (0.01ms, 3.75MB)
테스트 3 〉통과 (0.01ms, 4.28MB)
테스트 4 〉통과 (0.01ms, 4.33MB)
테스트 5 〉통과 (0.01ms, 4.26MB)
테스트 6 〉통과 (0.01ms, 4.25MB)
테스트 7 〉통과 (0.01ms, 4.3MB)
테스트 8 〉통과 (0.01ms, 3.66MB)
테스트 9 〉통과 (0.01ms, 4.27MB)
테스트 10 〉통과 (0.01ms, 4.32MB)
테스트 11 〉통과 (0.01ms, 4.33MB)
```

## 초기 작성한 코드

```cpp

```

### 초기테스트

```text
```
