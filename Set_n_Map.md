## 📚 집합과 맵 정리

## 🔍 핵심 개념

| 자료구조 | 목적 | 특징 |
|--------|------|------|
| **집합 (Set)** | 중복 제거, 원소 존재 여부 확인 | `add`, `remove`, `contains`, `size` |
| **맵 (Map)** | 키-값 쌍 저장, 키 기반 접근 | `insert`, `find`, `erase`, `get` |

---

## 📌 1. **집합 (Set)**

### 🎯 기능
- 원소를 저장하고 중복을 제거
- 원소가 존재하는지 확인
- 원소 추가/제거

### ✅ 1. 집합 (std::set)

```c
// set_example.c
#include <stdio.h>
#include <stdlib.h>
#include <string.h>
#include <set>
#include <iostream>

using namespace std;

int main() {
    set<int> s;

    // 원소 추가 (중복 제거 자동)
    s.insert(1);
    s.insert(2);
    s.insert(3);
    s.insert(2); // 중복 무시됨

    // 원소 존재 여부 확인
    if (s.find(2) != s.end()) {
        printf("Contains 2\n");
    }

    // 크기 확인
    printf("Set size: %d\n", s.size());

    // 원소 제거
    s.erase(2);

    printf("After remove 2: size = %d\n", s.size());

    return 0;
}
```

> ✅ 출력 예:
> 
> ```
> Contains 2  
> Set size: 3  
> After remove 2: size = 2
> ```

---

## 📌 2. **맵 (Map)**

### 🎯 기능
- 키-값 쌍 저장 (예: `key -> value`)
- 키 기반으로 값 가져오기
- 키 존재 여부 확인

### ✅ 2. 맵 (std::map)

```c
// map_example.c
#include <stdio.h>
#include <stdlib.h>
#include <string.h>
#include <map>
#include <iostream>

using namespace std;

int main() {
    map<int, int> m;

    // 키-값 추가 (중복 키는 오버라이드)
    m[1] = 100;
    m[2] = 200;
    m[3] = 300;

    // 키 기반 값 가져오기
    if (m.find(1) != m.end()) {
        printf("Map: key 1 -> %d\n", m[1]);
    }

    printf("Map: key 2 -> %d\n", m[2]);
    printf("Map size: %d\n", m.size());

    // 없는 키 접근
    printf("Map: key 4 -> %d\n", m.find(4) != m.end() ? m[4] : -1);

    // 원소 제거
    m.erase(2);

    printf("After remove 2: size = %d\n", m.size());

    return 0;
}
```

> ✅ 출력 예:
> 
> ```
> Map: key 1 -> 100  
> Map: key 2 -> 200  
> Map size: 3  
> Map: key 4 -> -1  
> After remove 2: size = 2
> ```

---

## 📊 비교 요약

| 기능 | 집합 (Set) | 맵 (Map) |
|------|-----------|----------|
| **기능** | 원소 존재 여부, 중복 제거 | 키-값 저장, 키 기반 접근 |
| **시간 복잡도 (검색)** | O(n) (최악) | O(n) (최악) |
| **효율성** | 중복 제거 가능 | 값에 접근 가능 |
| **응용** | 유니크 값 처리, 집합 연산 | 키 기반 데이터 저장 |

---

## 📌 핵심 팁

- **C 스타일은 메모리 관리 책임이 있음** → `malloc/free` 사용
- **중복 제거는 for-반복으로 처리** (효율성은 제한)
- **키-값 구조는 배열 기반으로 구현** (실제 프로젝트에서는 해시 테이블이 더 효율)
- **확장성**: `capacity`를 증가시켜 더 많은 원소 저장 가능

---

## 📚 학습 포인트

1. **집합 (Set)** – 중복 제거, 원소 존재 확인  
2. **맵 (Map)** – 키-값 저장, 값 접근  
3. **예제 코드 작성** – 실제 문제에 적용  
4. **효율성 개선** – 해시 테이블, 트리 구조로 확장
