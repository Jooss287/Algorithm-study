# 프린터

[Programmers 42587 문제](https://programmers.co.kr/learn/courses/30/lessons/42587)  

> Stack/Queue 문제로, 우선순위가 있는 프린터 대기열 중, 원하는 파일의 인쇄 순서를 알아내는 문제입니다.

## 메모 할 사항

index와 priority를 합친 구조체를 만들어 각 파일별로 관리합니다.
인쇄목록을 queue에 넣어 대기열을 구성하고, 대기열의 첫번째 파일마다 우선순위를 확인하고 해당되지 않는 우선순위일 경우 Queue에 다시 push합니다.

## 입출력 예시

priorities | location | return
|---|---|---|
[2,1,3,2] | 2 | 1
[1,1,9,1,1,1] | 0 | 5

## Result Code

```cpp
struct FILE_STRUC {
    int index;
    int priority;
    FILE_STRUC(int _index, int _priority) : index(_index), priority(_priority) {};
};

int solution(vector<int> priorities, int location) {
    int answer = 0;
    queue<FILE_STRUC> fileQueue;
    vector<int> orderedPriorty(priorities.begin(), priorities.end());
    sort(orderedPriorty.begin(), orderedPriorty.end(), greater<int>());
    int orderCnt = 0;

    for ( int i = 0; i < static_cast<int>(priorities.size()); i++)
    {
        fileQueue.push(FILE_STRUC(i, priorities[i]));
    }
    
    while(!fileQueue.empty())
    {
        auto file = fileQueue.front();
        fileQueue.pop();
        
        if ( file.priority < orderedPriorty[orderCnt] )
        {
            fileQueue.push(file);
        }
        else
        {
            if ( file.index == location )
            {
                answer = orderCnt+1;
                break;
            }
            orderCnt++;
        }
    }
    return answer;
}
```

### Result Code 테스트 결과

```text
정확성  테스트
테스트 1 〉통과 (0.01ms, 4.21MB)
테스트 2 〉통과 (0.02ms, 4.33MB)
테스트 3 〉통과 (0.02ms, 3.68MB)
테스트 4 〉통과 (0.01ms, 4.33MB)
테스트 5 〉통과 (0.01ms, 4.26MB)
테스트 6 〉통과 (0.01ms, 4.27MB)
테스트 7 〉통과 (0.01ms, 4.33MB)
테스트 8 〉통과 (0.02ms, 3.64MB)
테스트 9 〉통과 (0.01ms, 4.27MB)
테스트 10 〉통과 (0.01ms, 4.34MB)
테스트 11 〉통과 (0.01ms, 4.32MB)
테스트 12 〉통과 (0.01ms, 4.26MB)
테스트 13 〉통과 (0.02ms, 4.33MB)
테스트 14 〉통과 (0.01ms, 4.33MB)
테스트 15 〉통과 (0.01ms, 3.68MB)
테스트 16 〉통과 (0.01ms, 4.26MB)
테스트 17 〉통과 (0.01ms, 4.27MB)
테스트 18 〉통과 (0.01ms, 4.26MB)
테스트 19 〉통과 (0.01ms, 3.66MB)
테스트 20 〉통과 (0.01ms, 4.25MB)
```

## 초기 작성한 코드

```cpp

```

### 초기테스트

```text
```
