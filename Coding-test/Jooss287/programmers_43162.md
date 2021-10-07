# 네트워크

[Programmers 43162 문제](https://programmers.co.kr/learn/courses/30/lessons/43162)  

> DFS/BFS 문제로, 컴퓨터끼리 연결된 네트워크의 개수를 구하는 문제입니다.

## 메모 할 사항

재귀함수를 사용해서 DFS를 구현하였습니다.
연결된 네트워크를 DFS으로 Search를 하되, 이미 확인한 컴퓨터들을 지워가며 확인합니다.
한 번의 연결 searching이 종료되면 그것이 하나의 네트워크임을 확인 할 수 있습니다.

## 입출력 예시

n | computers | return
|---|---|---|
3 | [[1,1,0],[1,1,0],[0,0,1]] | 2
3 | [[1,1,0],[1,1,1],[0,1,1]] | 1

## Result Code

```cpp
void searchGraph(const vector<vector<int>> computers, vector<int> &comNumber, const int comIndex) {
    const vector<int> nowComputer = computers[comIndex];
    comNumber[comIndex] = 0;
    for ( int i = 0; i < static_cast<int>(nowComputer.size()); i++)
    {
        if ( i == comIndex)
            continue;

        if ( comNumber[i] == 0)
            continue;
        if ( nowComputer[i] == 1 )
            searchGraph(computers, comNumber, i);
    }
}

int solution(int n, vector<vector<int>> computers) {
    int answer = 0;
    vector<int> comNumber(computers.size(), 1);
    
    for ( int i = 0;i < static_cast<int>(computers.size()); i++)
    {
        if ( comNumber[i] == 0 )
            continue;
        searchGraph(computers, comNumber, i);
        answer++;
    }
    
    return answer;
}
```

### Result Code 테스트 결과

```text
정확성  테스트
테스트 1 〉통과 (0.01ms, 4.27MB)
테스트 2 〉통과 (0.01ms, 3.75MB)
테스트 3 〉통과 (0.04ms, 4.33MB)
테스트 4 〉통과 (0.04ms, 4.21MB)
테스트 5 〉통과 (0.01ms, 4.33MB)
테스트 6 〉통과 (0.40ms, 4.27MB)
테스트 7 〉통과 (0.02ms, 3.71MB)
테스트 8 〉통과 (0.27ms, 4.33MB)
테스트 9 〉통과 (0.12ms, 4.27MB)
테스트 10 〉통과 (0.13ms, 4.27MB)
테스트 11 〉통과 (2.35ms, 6.6MB)
테스트 12 〉통과 (2.01ms, 5.46MB)
테스트 13 〉통과 (0.48ms, 4.27MB)
```

## 초기 작성한 코드

```cpp

```

### 초기테스트

```text
```
