# 타겟 넘버

[Programmers 43165 문제](https://programmers.co.kr/learn/courses/30/lessons/43165)  

> DFS/BFS 문제로, 정수들을 더하고 빼서 타겟 넘버를 만드는 문제입니다.

## 메모 할 사항

재귀함수를 사용해서 DFS를 구현하였습니다.
앞에서부터 수를 더해나가야 하므로 경로의 특징을 가져야 하고 모든 경우의 수를 다 계산해야만 합니다.

## 입출력 예시

numbers | target | return
|---|---|---|
[1, 1, 1, 1, 1] | 3 | 5

## Result Code

```cpp
int dfs(const vector<int> numbers, const int target, const int stack, int sum) {
    
    int plusSum = sum + numbers[stack];
    int minusSum = sum - numbers[stack];
    
    int ret = 0;

    if ( numbers.size()-1 == stack)
    {
        if ( plusSum == target)
            ret++;
        if ( minusSum == target)
            ret++;
    }
    else {
        ret += dfs(numbers, target, stack+1, plusSum);
        ret += dfs(numbers, target, stack+1, minusSum);
    }
    return ret;
}

int solution(vector<int> numbers, int target) {
    int answer = 0;
    
    answer = dfs(numbers, target, 0, 0);
    
    return answer;
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

```

### 초기테스트

```text
```
