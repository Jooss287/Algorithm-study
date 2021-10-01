# 소수 찾기

[Programmers 42842 문제](https://programmers.co.kr/learn/courses/30/lessons/42842)  

> 완전탐색(Exhaustive search) bruce-force search 라고도 하며 무식하게 모든 탐색을 하는 문제입니다.

## 메모 할 사항

1. brown 카펫 기준으로 수식을 풀어서 최소 가로 brown 길이를 구합니다.
2. brown 세로 길이가 최소 3은 되어야 하므로, 최대 세로 길이부터 최소 길이까지 loop를 돌며 yellow 칸 개수를 비교합니다.

## 입출력 예시

brwon | yello | return
|---|---|---|
10 | 2 | [4, 3]
8 | 1 | [3, 3]
24 | 24 | [8, 6]

## Result Code

```cpp
vector<int> solution(int brown, int yellow) {
    vector<int> answer;
    int brownRange = (brown + 4) / 2;
    int brownWidth = ceil(brownRange / 2.);
    int brownHeight = brownRange - brownWidth;

    while(brownHeight >= 3)
    {
        int yellowSize = (brownWidth-2) * (brownHeight-2);
        if ( yellowSize == yellow)
            break;

        brownWidth++;
        brownHeight--;
    }
    
    answer.push_back(brownWidth);
    answer.push_back(brownHeight);

    return answer;
}
```

### Result Code 테스트 결과

```text
테스트 1 〉 통과 (0.01ms, 4.26MB)
테스트 2 〉 통과 (0.01ms, 4.33MB)
테스트 3 〉 통과 (0.01ms, 3.68MB)
테스트 4 〉 통과 (0.01ms, 4.26MB)
테스트 5 〉 통과 (0.01ms, 3.66MB)
테스트 6 〉 통과 (0.01ms, 4.27MB)
테스트 7 〉 통과 (0.01ms, 3.66MB)
테스트 8 〉 통과 (0.01ms, 4.33MB)
테스트 9 〉 통과 (0.01ms, 4.33MB)
테스트 10 〉 통과 (0.01ms, 4.32MB)
테스트 11 〉 통과 (0.01ms, 4.33MB)
테스트 12 〉 통과 (0.01ms, 4.33MB)
테스트 13 〉 통과 (0.01ms, 4.21MB)
```

## 초기 작성한 코드

```cpp

```

### 초기테스트

```text
```
