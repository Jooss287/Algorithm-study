# 베스트앨범

[Programmers 42579 문제](https://programmers.co.kr/learn/courses/30/lessons/42579)  

> Hash 문제로 장르, 노래, 고유번호 순서로 각자의 정렬기준으로 정렬하여 답을 도출하는 문제입니다.

## 메모 할 사항

map을 통하여 string들의 접근을 빠르게 하였고, set과 pair를 통하여 임의의 정렬을 구현하였습니다.

* Operator의 사용 조건을 명확하게 이해해야 합니다.

## 입출력 예시

genres | plays | return
|---|---|---|
["classic", "pop", "classic", "classic", "pop] | [500, 600, 150, 800, 2500] | [4, 1, 3, 0]

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
