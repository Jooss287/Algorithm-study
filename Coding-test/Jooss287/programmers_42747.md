# H-Index

[Programmers 42747 문제](https://programmers.co.kr/learn/courses/30/lessons/42747)  

> 정렬(sort)문제로 논문의 H-Index를 구하는 문제입니다.

## 메모 할 사항

논문의 citations를 내림차순 정렬해서 h-index를 구합니다.
sort된 배열만으로 h-index초기값을 구한 뒤 1씩 증가시켜 가면서 조건을 파악합니다.

## 입출력 예시

citations | return
|---|---|
[3, 0, 6, 1, 5] | 3
[3, 0, 6, 1, 5, 5, 5] | 4
[2, 2] | 2
[3, 3] | 2

## Result Code

```cpp
bool isH_Index(const vector<int> citations, int index)
{
    return citations[index-1] >= index;
}

int solution(vector<int> citations) {
    int answer = 0;
    int cnt = 0;
    sort(citations.begin(), citations.end(), std::greater<int>());

    for ( int i = 0; i < static_cast<int>(citations.size()); i++)
    {
        int cit = citations[i];
        if ( cit > citations.size())
            continue;
        if ( cit == 0 )
            continue;

        if ( isH_Index(citations, cit) )
        {
            cnt = i;
            break;
        }
    }

    answer = cnt + 1;
    while( isH_Index(citations, answer) )
    {    
        answer++;
    }

    return answer-1;
}
```

### Result Code 테스트 결과

```text
테스트 1 〉통과 (0.03ms, 4.33MB)
테스트 2 〉통과 (0.05ms, 4.32MB)
테스트 3 〉통과 (0.04ms, 3.66MB)
테스트 4 〉통과 (0.03ms, 4.25MB)
테스트 5 〉통과 (0.04ms, 4.26MB)
테스트 6 〉통과 (0.06ms, 4.33MB)
테스트 7 〉통과 (0.03ms, 4.25MB)
테스트 8 〉통과 (0.01ms, 4.26MB)
테스트 9 〉통과 (0.03ms, 4.32MB)
테스트 10 〉 통과 (0.02ms, 4.27MB)
테스트 11 〉통과 (0.06ms, 3.69MB)
테스트 12 〉통과 (0.02ms, 3.66MB)
테스트 13 〉통과 (0.06ms, 4.28MB)
테스트 14 〉통과 (0.05ms, 4.21MB)
테스트 15 〉통과 (0.05ms, 4.32MB)
테스트 16 〉통과 (0.01ms, 4.32MB)
```

## 초기 작성한 코드

```cpp
bool isH_Index(const vector<int> citations, int index)
{
    return citations[index-1] >= index;
}

int solution(vector<int> citations) {
    int answer = 0;
    int cnt = 0;
    sort(citations.begin(), citations.end(), std::greater<int>());

    for ( int i = 0; i < static_cast<int>(citations.size()); i++)
    {
        int cit = citations[i];
        if ( cit > citations.size())
            continue;
        if ( cit == 0 )
            continue;

        if ( isH_Index(citations, cit) )
        {
            int val = i + 1;
            while( isH_Index(citations, val) )
            {    
                val++;
            }

            answer = val-1;
            break;
        }
    }

    return answer;
}
```

### 초기테스트

```text
테스트 1 〉 통과 (0.02ms, 4.32MB)
테스트 2 〉 통과 (0.04ms, 4.27MB)
테스트 3 〉 통과 (0.04ms, 3.71MB)
테스트 4 〉 통과 (0.03ms, 4.33MB)
테스트 5 〉 통과 (0.04ms, 4.32MB)
테스트 6 〉 통과 (0.05ms, 4.26MB)
테스트 7 〉 통과 (0.03ms, 3.7MB)
테스트 8 〉 통과 (0.01ms, 3.66MB)
테스트 9 〉 실패 (0.01ms, 3.69MB)
테스트 10 〉 통과 (0.03ms, 3.69MB)
테스트 11 〉 통과 (0.05ms, 4.32MB)
테스트 12 〉 통과 (0.01ms, 4.33MB)
테스트 13 〉 통과 (0.06ms, 4.26MB)
테스트 14 〉 통과 (0.05ms, 4.27MB)
테스트 15 〉 통과 (0.04ms, 4.34MB)
테스트 16 〉 통과 (0.01ms, 4.26MB)
```
