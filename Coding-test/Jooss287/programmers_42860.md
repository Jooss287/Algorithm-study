# 소수 찾기

[Programmers 42860 문제](https://programmers.co.kr/learn/courses/30/lessons/42860)  

> 탐욕법(Greed) 최소 조이스틱 움직임을 통해 알파벳 이름을 완성하는 문제입니다.

## 메모 할 사항

1. 기준 진행방향(오른쪽)에서 두번째 문자가 A일시 반대쪽 방향을 선택합니다.
2. 진행방향을 지정하고 마지막 문자가 A일시 움직임을 1회 줄여야 합니다.

* 탐욕법은 매 선택의 순간에 가장 최적의 선택이 최고의 결과를 얻을 수 있도록 유도하는 알고리즘입니다.
* 그러므로 기준점에서 좌, 우로 search하여 가장 최소의 움직임을 찾고 그 방향으로 선택합니다.
* 해당 문제는 프로그래머스 내부 질문하기에서도 문제와 정답이 이상하다는 의견이 분분합니다. 문제풀이와 몇가지 테스트 케이스만 확인하고 다음 문제로 넘어가겠습니다.

## 입출력 예시

name | return
|---|---|
"JEROEN" | 56
"JAN" | 23

## Result Code

```cpp
int changeTextJoyStick(const char txt)
{
    int A2Target = txt - 'A';
    int Z2Target = 'Z' + 1 - txt;
    int stickMove = A2Target < Z2Target ? A2Target : Z2Target;
    return stickMove;
}

void outOfRange(int &pointer, const string name)
{
    if ( pointer < 0)
        pointer = name.size() + pointer;
    else if ( pointer >= name.size() )
        pointer = pointer - name.size();
}

int searchLeastMoveJoystick(const string name, const string base, const int nowPoint, int direction, int &directionMove, int &changeMove)
{
    int pt = nowPoint + direction;
    int a_count = 1;

    outOfRange(pt, name);
    while((name[pt] == 'A') || (name[pt] == base[pt]))
    {
        a_count++;
        pt += direction;
        outOfRange(pt, name);
    }
    
    directionMove = a_count;
    changeMove = changeTextJoyStick(name[pt]);
    return directionMove + changeMove;
}

int solution(string name) {
    int answer = 0;
    string base(name.size(), 'A');
    int size = name.size();
    int direction = 1;
    int pointer = 0;

    answer += changeTextJoyStick(name[pointer]);
    base[pointer] = name[pointer];

    while(name.compare(base) != 0)
    {
        int plusDirectionMove = 0;
        int plusChangeMove = 0;
        int plusDirectionSize = searchLeastMoveJoystick(name, base, pointer, 1, plusDirectionMove, plusChangeMove);
        int minusDirectionMove = 0;
        int minusChangeMove = 0;
        int minusDirectionSize = searchLeastMoveJoystick(name, base, pointer, -1, minusDirectionMove, minusChangeMove);

        if ( plusDirectionSize <= minusDirectionSize)
        {
            pointer += plusDirectionMove;
            outOfRange(pointer, name);
            answer += plusDirectionSize;
        }
        else
        {
            pointer -= minusDirectionMove;
            outOfRange(pointer, name);
            answer += minusDirectionSize;
        }
        base[pointer] = name[pointer];
    }

    return answer;
}
```

### Result Code 테스트 결과

```text
테스트 1 〉 통과 (0.01ms, 4.25MB)
테스트 2 〉 통과 (0.01ms, 4.32MB)
테스트 3 〉 통과 (0.01ms, 3.62MB)
테스트 4 〉 실패 (0.02ms, 4.27MB)
테스트 5 〉 실패 (0.01ms, 4.21MB)
테스트 6 〉 통과 (0.01ms, 4.27MB)
테스트 7 〉 실패 (0.02ms, 4.21MB)
테스트 8 〉 통과 (0.01ms, 4.26MB)
테스트 9 〉 실패 (0.01ms, 4.33MB)
테스트 10 〉 통과 (0.01ms, 4.27MB)
테스트 11 〉 통과 (0.01ms, 3.66MB)
```

## 초기 작성한 코드

```cpp
void outOfRange(int &pointer, const string name)
{
    if ( pointer < 0)
            pointer = name.size()-1;
    if ( pointer >= name.size() )
        pointer = 0;
}

int countEndOfA(const string name, int direction)
{
    int pt = 0 - direction;
    int a_count = 0;

    outOfRange(pt, name);

    while(name[pt] == 'A')
    {
        a_count++;
        pt -= direction;
        outOfRange(pt, name);
    }
    return a_count;
}

int solution(string name) {
    int answer = 0;
    string base(name.size(), 'A');
    int size = name.size();
    int direction = 1;
    int pointer = 0;

    //direciotn 설정
    int plusDirecionSize = countEndOfA(name, 1);
    int minusDirectionsize = countEndOfA(name, -1);

    if ( plusDirecionSize >= minusDirectionsize)
    {
        direction = 1;
        size = name.size() - plusDirecionSize;
    }
    else
    {
        direction = -1;
        size = name.size() - minusDirectionsize;
    }

    for(int i =0; i < size; i++)
    {
        int A2Target = name[pointer] - 'A';
        int Z2Target = 'Z' + 1 - name[pointer];
        int stick = A2Target < Z2Target ? A2Target : Z2Target;
        base[pointer] = name[pointer];
        answer += stick;
        
        // cout << stick << "\t";
        if( name.compare(base) == 0)
            break;
        
        //move
        pointer += direction;
        outOfRange(pointer, name);
        answer++;
    }
    
    return answer;
}
```

### 초기테스트

```text
테스트 1 〉 통과 (0.02ms, 4.33MB)
테스트 2 〉 통과 (0.02ms, 4.33MB)
테스트 3 〉 통과 (0.02ms, 3.71MB)
테스트 4 〉 통과 (0.02ms, 4.33MB)
테스트 5 〉 통과 (0.02ms, 4.33MB)
테스트 6 〉 통과 (0.02ms, 4.26MB)
테스트 7 〉 통과 (0.02ms, 4.27MB)
테스트 8 〉 통과 (0.02ms, 4.33MB)
테스트 9 〉 통과 (0.02ms, 4.33MB)
테스트 10 〉 통과 (0.02ms, 4.34MB)
테스트 11 〉 실패 (0.02ms, 4.27MB)
```
