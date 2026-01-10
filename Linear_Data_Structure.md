## 선형 자료구조와 C++ STL

### 목차

1.  **선형 자료구조의 이해**
    *   1.1. 선형 자료구조란?
    *   1.2. 선형 자료구조의 특징
    *   1.3. 선형 자료구조의 종류
2.  **C++ STL (Standard Template Library) 소개**
    *   2.1. STL의 개요
    *   2.2. STL의 구성 요소 (컨테이너, 알고리즘, 반복자)
    *   2.3. STL 사용의 이점
3.  **C++ STL 컨테이너를 활용한 선형 자료구조 구현**
    *   3.1. `std::vector`
        *   3.1.1. 개념 및 특징
        *   3.1.2. 주요 연산 및 시간 복잡도
        *   3.1.3. 실무 적용 예시 (동적 배열)
    *   3.2. `std::deque`
        *   3.2.1. 개념 및 특징
        *   3.2.2. 주요 연산 및 시간 복잡도
        *   3.2.3. 실무 적용 예시 (양방향 큐)
    *   3.3. `std::list`
        *   3.3.1. 개념 및 특징
        *   3.3.2. 주요 연산 및 시간 복잡도
        *   3.3.3. 실무 적용 예시 (연결 리스트)
    *   3.4. `std::forward_list`
        *   3.4.1. 개념 및 특징
        *   3.4.2. 주요 연산 및 시간 복잡도
        *   3.4.3. 실무 적용 예시 (단방향 연결 리스트)
    *   3.5. `std::stack` (컨테이너 어댑터)
        *   3.5.1. 개념 및 특징
        *   3.5.2. 주요 연산 및 시간 복잡도
        *   3.5.3. 실무 적용 예시 (스택)
    *   3.6. `std::queue` (컨테이너 어댑터)
        *   3.6.1. 개념 및 특징
        *   3.6.2. 주요 연산 및 시간 복잡도
        *   3.6.3. 실무 적용 예시 (큐)
    *   3.7. `std::priority_queue` (컨테이너 어댑터)
        *   3.7.1. 개념 및 특징
        *   3.7.2. 주요 연산 및 시간 복잡도
        *   3.7.3. 실무 적용 예시 (우선순위 큐)
4.  **선형 자료구조의 응용 및 알고리즘**
    *   4.1. 배열 기반 알고리즘
    *   4.2. 연결 리스트 기반 알고리즘
    *   4.3. 스택 및 큐를 활용한 문제 해결
5.  **STL 사용 시 고려사항 및 팁**
    *   5.1. 적절한 컨테이너 선택 기준
    *   5.2. 반복자(Iterator)의 이해와 활용
    *   5.3. 메모리 관리 및 성능 최적화
    *   5.4. 자주 발생하는 오류 및 디버깅

---

### 1. 선형 자료구조의 이해

#### 1.1. 선형 자료구조란?

선형 자료구조(Linear Data Structure)는 데이터를 순차적으로 저장하고 접근하는 자료구조를 말합니다. 각 데이터 요소는 이전 요소와 다음 요소에 대한 관계를 가지며, 이러한 관계는 일직선 형태로 표현될 수 있습니다. 즉, 데이터들이 일렬로 나열되어 있는 형태를 띠고 있습니다.

#### 1.2. 선형 자료구조의 특징

*   **순차적 저장:** 데이터가 메모리 상에 순서대로 저장됩니다.
*   **단일 경로:** 각 데이터 요소는 최대 하나의 이전 요소와 하나의 다음 요소를 가집니다. (단, 시작과 끝 요소는 예외)
*   **접근 용이성:** 특정 위치의 데이터에 접근하기 비교적 쉽습니다.
*   **구현 용이성:** 개념적으로 이해하고 구현하기 쉽습니다.

#### 1.3. 선형 자료구조의 종류

*   **배열 (Array):** 고정된 크기를 가지며, 동일한 타입의 데이터를 연속된 메모리 공간에 저장합니다. 인덱스를 통해 직접 접근이 가능합니다.
*   **연결 리스트 (Linked List):** 각 데이터 요소(노드)가 데이터와 다음 노드를 가리키는 포인터를 함께 저장합니다. 동적인 크기 조절이 용이하며, 삽입/삭제가 효율적입니다.
    *   단일 연결 리스트 (Singly Linked List)
    *   이중 연결 리스트 (Doubly Linked List)
*   **스택 (Stack):** LIFO(Last-In, First-Out) 구조로, 가장 최근에 삽입된 데이터가 가장 먼저 삭제됩니다.
*   **큐 (Queue):** FIFO(First-In, First-Out) 구조로, 가장 먼저 삽입된 데이터가 가장 먼저 삭제됩니다.

### 2. C++ STL (Standard Template Library) 소개

#### 2.1. STL의 개요

C++ STL은 C++ 표준 라이브러리의 핵심 부분으로, 일반적인 프로그래밍 작업을 위한 다양한 자료구조와 알고리즘을 제공합니다. STL은 템플릿(Template)을 기반으로 하여, 다양한 데이터 타입에 대해 일반화된 방식으로 사용할 수 있습니다.

#### 2.2. STL의 구성 요소

STL은 크게 세 가지 주요 구성 요소로 나뉩니다.

*   **컨테이너 (Containers):** 데이터를 저장하는 객체입니다. (예: `vector`, `list`, `map`)
*   **알고리즘 (Algorithms):** 컨테이너의 요소들을 조작하는 함수입니다. (예: `sort`, `find`, `copy`)
*   **반복자 (Iterators):** 컨테이너의 요소들에 접근하고 순회하는 방법을 제공하는 객체입니다. (예: `vector::iterator`)

#### 2.3. STL 사용의 이점

*   **재사용성:** 이미 검증된 라이브러리를 사용하여 개발 시간을 단축합니다.
*   **효율성:** STL은 고도로 최적화되어 있어 성능이 뛰어납니다.
*   **일관성:** 표준화된 인터페이스를 제공하여 코드의 가독성과 유지보수성을 높입니다.
*   **템플릿 기반:** 다양한 데이터 타입에 대해 유연하게 사용할 수 있습니다.

### 3. C++ STL 컨테이너를 활용한 선형 자료구조 구현

#### 3.1. `std::vector`

`std::vector`는 동적으로 크기가 조절되는 배열입니다. STL에서 가장 널리 사용되는 컨테이너 중 하나입니다.

*   **3.1.1. 개념 및 특징**
    *   연속된 메모리 공간에 요소를 저장합니다.
    *   크기가 동적으로 조절됩니다. (필요시 메모리 재할당 및 요소 복사 발생)
    *   인덱스를 통한 임의 접근(Random Access)이 O(1) 시간에 가능합니다.
    *   끝에 요소를 추가하거나 삭제하는 연산이 평균 O(1) 시간 복잡도를 가집니다. (재할당 시 O(n))

*   **3.1.2. 주요 연산 및 시간 복잡도**

| 연산             | 시간 복잡도 | 설명                                   |
| :--------------- | :---------- | :------------------------------------- |
| `push_back(val)` | 평균 O(1)   | 벡터 끝에 요소 추가                    |
| `pop_back()`     | O(1)        | 벡터 끝 요소 삭제                      |
| `insert(pos, val)` | O(n)        | 특정 위치에 요소 삽입 (이후 요소 이동) |
| `erase(pos)`     | O(n)        | 특정 위치 요소 삭제 (이후 요소 이동)   |
| `operator[](idx)`| O(1)        | 인덱스로 요소 접근                     |
| `at(idx)`        | O(1)        | 인덱스로 요소 접근 (범위 검사 포함)    |
| `size()`         | O(1)        | 요소 개수 반환                         |
| `empty()`        | O(1)        | 벡터가 비어 있는지 확인                |
| `clear()`        | O(n)        | 모든 요소 삭제                         |

*   **3.1.3. 실무 적용 예시 (동적 배열)**

```cpp
#include <iostream>
#include <vector>

int main() {
    std::vector<int> numbers; // 정수형 벡터 선언

    // 요소 추가
    numbers.push_back(10);
    numbers.push_back(20);
    numbers.push_back(30);

    // 벡터 크기 확인
    std::cout << "Size: " << numbers.size() << std::endl; // 출력: Size: 3

    // 인덱스로 요소 접근
    std::cout << "Element at index 1: " << numbers[1] << std::endl; // 출력: Element at index 1: 20

    // 반복자를 이용한 순회
    std::cout << "Elements: ";
    for (std::vector<int>::iterator it = numbers.begin(); it != numbers.end(); ++it) {
        std::cout << *it << " "; // 출력: Elements: 10 20 30
    }
    std::cout << std::endl;

    // 특정 위치에 삽입
    numbers.insert(numbers.begin() + 1, 15); // 1번 인덱스에 15 삽입

    // 요소 삭제
    numbers.pop_back(); // 마지막 요소(30) 삭제

    std::cout << "Updated Elements: ";
    for (int num : numbers) { // 범위 기반 for 루프
        std::cout << num << " "; // 출력: Updated Elements: 10 15 20
    }
    std::cout << std::endl;

    return 0;
}
```

#### 3.2. `std::deque`

`std::deque` (double-ended queue)는 양쪽 끝에서 삽입 및 삭제가 효율적인 동적 배열입니다. `vector`와 유사하지만, 양쪽 끝에서의 연산이 O(1)에 가깝습니다.

*   **3.2.1. 개념 및 특징**
    *   메모리 상에 연속적이지 않은 여러 개의 청크(chunk)로 나뉘어 저장될 수 있습니다.
    *   양쪽 끝에서의 삽입 및 삭제가 O(1) 시간에 가능합니다.
    *   인덱스를 통한 임의 접근이 가능하지만, `vector`보다 약간 느릴 수 있습니다 (O(1)이지만 상수 인자가 더 큼).

*   **3.2.2. 주요 연산 및 시간 복잡도**

| 연산             | 시간 복잡도 | 설명                                   |
| :--------------- | :---------- | :------------------------------------- |
| `push_back(val)` | O(1)        | 뒤에 요소 추가                         |
| `pop_back()`     | O(1)        | 뒤에 요소 삭제                         |
| `push_front(val)`| O(1)        | 앞에 요소 추가                         |
| `pop_front()`    | O(1)        | 앞에 요소 삭제                         |
| `insert(pos, val)` | O(n)        | 특정 위치에 요소 삽입 (양쪽에서 가까운 쪽으로 이동) |
| `erase(pos)`     | O(n)        | 특정 위치 요소 삭제 (양쪽에서 가까운 쪽으로 이동)   |
| `operator[](idx)`| O(1)        | 인덱스로 요소 접근                     |
| `at(idx)`        | O(1)        | 인덱스로 요소 접근 (범위 검사 포함)    |
| `size()`         | O(1)        | 요소 개수 반환                         |
| `empty()`        | O(1)        | 비어 있는지 확인                       |

*   **3.2.3. 실무 적용 예시 (양방향 큐)**

```cpp
#include <iostream>
#include <deque>

int main() {
    std::deque<int> dq;

    dq.push_back(10);    // dq: [10]
    dq.push_front(5);    // dq: [5, 10]
    dq.push_back(20);    // dq: [5, 10, 20]

    std::cout << "Front element: " << dq.front() << std::endl; // 출력: Front element: 5
    std::cout << "Back element: " << dq.back() << std::endl;   // 출력: Back element: 20

    dq.pop_front();      // dq: [10, 20]
    dq.pop_back();       // dq: [10]

    std::cout << "Deque elements: ";
    for (int val : dq) {
        std::cout << val << " "; // 출력: Deque elements: 10
    }
    std::cout << std::endl;

    return 0;
}
```

#### 3.3. `std::list`

`std::list`는 이중 연결 리스트(Doubly Linked List)를 구현한 컨테이너입니다. 각 요소는 이전 요소와 다음 요소를 가리키는 포인터를 가집니다.

*   **3.3.1. 개념 및 특징**
    *   요소들이 메모리 상에 연속적으로 저장되지 않습니다.
    *   삽입 및 삭제 연산이 매우 효율적입니다 (O(1)).
    *   임의 접근(인덱스를 통한 접근)은 지원하지 않으며, 순차 접근만 가능합니다. (반복자를 이용해야 함)
    *   `vector`나 `deque`에 비해 메모리 오버헤드가 큽니다 (각 노드마다 포인터 저장 공간 필요).

*   **3.3.2. 주요 연산 및 시간 복잡도**

| 연산             | 시간 복잡도 | 설명                                   |
| :--------------- | :---------- | :------------------------------------- |
| `push_back(val)` | O(1)        | 뒤에 요소 추가                         |
| `pop_back()`     | O(1)        | 뒤에 요소 삭제                         |
| `push_front(val)`| O(1)        | 앞에 요소 추가                         |
| `pop_front()`    | O(1)        | 앞에 요소 삭제                         |
| `insert(pos, val)` | O(1)        | 반복자가 가리키는 위치 앞에 요소 삽입   |
| `erase(pos)`     | O(1)        | 반복자가 가리키는 요소 삭제            |
| `size()`         | O(1)        | 요소 개수 반환 (C++11부터 O(1) 보장)   |
| `empty()`        | O(1)        | 비어 있는지 확인                       |
| `splice()`       | O(1)        | 다른 리스트의 요소를 이동 (효율적)     |

*   **3.3.3. 실무 적용 예시 (연결 리스트)**

```cpp
#include <iostream>
#include <list>

int main() {
    std::list<int> myList;

    myList.push_back(10); // myList: [10]
    myList.push_front(5); // myList: [5, 10]
    myList.push_back(20); // myList: [5, 10, 20]

    // 반복자를 이용한 순회
    std::cout << "List elements: ";
    for (std::list<int>::iterator it = myList.begin(); it != myList.end(); ++it) {
        std::cout << *it << " "; // 출력: List elements: 5 10 20
    }
    std::cout << std::endl;

    // 특정 위치에 삽입 (2번째 요소 앞에 7 삽입)
    auto it = myList.begin();
    std::advance(it, 1); // it가 10을 가리키도록 이동
    myList.insert(it, 7); // myList: [5, 7, 10, 20]

    // 요소 삭제 (10 삭제)
    it = myList.begin();
    std::advance(it, 2); // it가 10을 가리키도록 이동
    myList.erase(it);    // myList: [5, 7, 20]

    std::cout << "Updated list elements: ";
    for (int val : myList) {
        std::cout << val << " "; // 출력: Updated list elements: 5 7 20
    }
    std::cout << std::endl;

    return 0;
}
```

#### 3.4. `std::forward_list`

`std::forward_list`는 단일 연결 리스트(Singly Linked List)를 구현한 컨테이너입니다. `std::list`와 유사하지만, 이전 노드를 가리키는 포인터가 없어 메모리 사용량이 더 적습니다.

*   **3.4.1. 개념 및 특징**
    *   각 요소는 다음 요소만 가리킵니다.
    *   삽입 및 삭제 연산이 효율적입니다 (O(1)).
    *   `std::list`와 마찬가지로 임의 접근은 지원하지 않습니다.
    *   `std::list`보다 더 적은 메모리를 사용합니다.
    *   `insert_after`, `erase_after`와 같은 메서드를 사용합니다.

*   **3.4.2. 주요 연산 및 시간 복잡도**

| 연산             | 시간 복잡도 | 설명                                   |
| :--------------- | :---------- | :------------------------------------- |
| `push_front(val)`| O(1)        | 앞에 요소 추가                         |
| `pop_front()`    | O(1)        | 앞에 요소 삭제                         |
| `insert_after(pos, val)` | O(1)        | 반복자가 가리키는 위치 뒤에 요소 삽입   |
| `erase_after(pos)` | O(1)        | 반복자가 가리키는 위치 다음 요소 삭제    |
| `size()`         | O(n)        | 요소 개수 반환 (O(n)이므로 주의)       |
| `empty()`        | O(1)        | 비어 있는지 확인                       |

*   **3.4.3. 실무 적용 예시 (단방향 연결 리스트)**

```cpp
#include <iostream>
#include <forward_list>

int main() {
    std::forward_list<int> flist;

    flist.push_front(20); // flist: [20]
    flist.push_front(10); // flist: [10, 20]
    flist.push_front(5);  // flist: [5, 10, 20]

    // 반복자를 이용한 순회
    std::cout << "Forward list elements: ";
    for (int val : flist) {
        std::cout << val << " "; // 출력: Forward list elements: 5 10 20
    }
    std::cout << std::endl;

    // 특정 위치 뒤에 삽입 (10 뒤에 15 삽입)
    auto it = flist.begin();
    std::advance(it, 1); // it가 10을 가리키도록 이동
    flist.insert_after(it, 15); // flist: [5, 10, 15, 20]

    // 특정 위치 다음 요소 삭제 (15 삭제)
    it = flist.begin();
    std::advance(it, 2); // it가 15를 가리키도록 이동
    flist.erase_after(it); // flist: [5, 10, 20]

    std::cout << "Updated forward list elements: ";
    for (int val : flist) {
        std::cout << val << " "; // 출력: Updated forward list elements: 5 10 20
    }
    std::cout << std::endl;

    return 0;
}
```

#### 3.5. `std::stack` (컨테이너 어댑터)

`std::stack`은 스택(Stack) 자료구조를 구현하는 컨테이너 어댑터입니다. 기본적으로 `std::deque`를 사용하지만, `std::vector`나 `std::list`를 기반으로 사용할 수도 있습니다. LIFO(Last-In, First-Out) 원칙을 따릅니다.

*   **3.5.1. 개념 및 특징**
    *   데이터는 'top'에서만 삽입(`push`)되고 삭제(`pop`)됩니다.
    *   가장 최근에 삽입된 요소가 가장 먼저 제거됩니다.
    *   `top()` 연산으로 가장 위에 있는 요소에 접근할 수 있습니다.

*   **3.5.2. 주요 연산 및 시간 복잡도**

| 연산     | 시간 복잡도 | 설명                 |
| :------- | :---------- | :------------------- |
| `push(val)`| O(1)        | 스택에 요소 추가     |
| `pop()`  | O(1)        | 스택에서 요소 제거   |
| `top()`  | O(1)        | 스택의 최상단 요소 반환 |
| `size()` | O(1)        | 요소 개수 반환       |
| `empty()`| O(1)        | 스택이 비어 있는지 확인 |

*   **3.5.3. 실무 적용 예시 (스택)**

```cpp
#include <iostream>
#include <stack>
#include <vector> // std::stack의 기본 컨테이너로 사용 가능

int main() {
    std::stack<int> s; // 기본적으로 std::deque 사용
    // std::stack<int, std::vector<int>> s_vec; // std::vector 기반 스택

    s.push(10); // s: [10]
    s.push(20); // s: [10, 20]
    s.push(30); // s: [10, 20, 30] (30이 top)

    std::cout << "Top element: " << s.top() << std::endl; // 출력: Top element: 30

    s.pop(); // 30 제거. s: [10, 20]
    std::cout << "Top element after pop: " << s.top() << std::endl; // 출력: Top element after pop: 20

    std::cout << "Stack size: " << s.size() << std::endl; // 출력: Stack size: 2

    while (!s.empty()) {
        std::cout << "Popping: " << s.top() << std::endl;
        s.pop();
    }
    // 출력:
    // Popping: 20
    // Popping: 10

    return 0;
}
```

#### 3.6. `std::queue` (컨테이너 어댑터)

`std::queue`는 큐(Queue) 자료구조를 구현하는 컨테이너 어댑터입니다. 기본적으로 `std::deque`를 사용하며, FIFO(First-In, First-Out) 원칙을 따릅니다.

*   **3.6.1. 개념 및 특징**
    *   데이터는 'back'으로 삽입(`push`)되고 'front'에서 삭제(`pop`)됩니다.
    *   가장 먼저 삽입된 요소가 가장 먼저 제거됩니다.
    *   `front()` 연산으로 가장 앞에 있는 요소에 접근하고, `back()`으로 가장 뒤에 있는 요소에 접근할 수 있습니다.

*   **3.6.2. 주요 연산 및 시간 복잡도**

| 연산     | 시간 복잡도 | 설명                 |
| :------- | :---------- | :------------------- |
| `push(val)`| O(1)        | 큐에 요소 추가       |
| `pop()`  | O(1)        | 큐에서 요소 제거     |
| `front()`| O(1)        | 큐의 맨 앞 요소 반환 |
| `back()` | O(1)        | 큐의 맨 뒤 요소 반환 |
| `size()` | O(1)        | 요소 개수 반환       |
| `empty()`| O(1)        | 큐가 비어 있는지 확인 |

*   **3.6.3. 실무 적용 예시 (큐)**

```cpp
#include <iostream>
#include <queue>
#include <vector> // std::queue의 기본 컨테이너로 사용 가능

int main() {
    std::queue<int> q; // 기본적으로 std::deque 사용
    // std::queue<int, std::vector<int>> q_vec; // std::vector 기반 큐

    q.push(10); // q: [10]
    q.push(20); // q: [10, 20]
    q.push(30); // q: [10, 20, 30] (10이 front)

    std::cout << "Front element: " << q.front() << std::endl; // 출력: Front element: 10
    std::cout << "Back element: " << q.back() << std::endl;   // 출력: Back element: 30

    q.pop(); // 10 제거. q: [20, 30]
    std::cout << "Front element after pop: " << q.front() << std::endl; // 출력: Front element after pop: 20

    std::cout << "Queue size: " << q.size() << std::endl; // 출력: Queue size: 2

    while (!q.empty()) {
        std::cout << "Dequeuing: " << q.front() << std::endl;
        q.pop();
    }
    // 출력:
    // Dequeuing: 20
    // Dequeuing: 30

    return 0;
}
```

#### 3.7. `std::priority_queue` (컨테이너 어댑터)

`std::priority_queue`는 우선순위 큐를 구현하는 컨테이너 어댑터입니다. 기본적으로 `std::vector`를 사용하며, `std::less` (최대 힙) 또는 `std::greater` (최소 힙)를 사용하여 요소의 우선순위를 결정합니다.

*   **3.7.1. 개념 및 특징**
    *   가장 높은 우선순위(기본값: 가장 큰 값)를 가진 요소가 항상 맨 앞에 위치합니다.
    *   `push` 연산은 요소를 삽입하고 힙 속성을 유지합니다.
    *   `pop` 연산은 가장 높은 우선순위의 요소를 제거합니다.
    *   `top()` 연산으로 가장 높은 우선순위의 요소에 접근할 수 있습니다.

*   **3.7.2. 주요 연산 및 시간 복잡도**

| 연산     | 시간 복잡도 | 설명                     |
| :------- | :---------- | :----------------------- |
| `push(val)`| O(log n)    | 우선순위 큐에 요소 추가  |
| `pop()`  | O(log n)    | 최상단 요소 제거         |
| `top()`  | O(1)        | 최상단 요소 반환         |
| `size()` | O(1)        | 요소 개수 반환           |
| `empty()`| O(1)        | 우선순위 큐가 비어 있는지 확인 |

*   **3.7.3. 실무 적용 예시 (우선순위 큐)**

```cpp
#include <iostream>
#include <queue>
#include <vector>

int main() {
    // 최대 힙 (기본값)
    std::priority_queue<int> max_heap;
    max_heap.push(10);
    max_heap.push(30);
    max_heap.push(20);
    max_heap.push(5);

    std::cout << "Max Heap Top: " << max_heap.top() << std::endl; // 출력: Max Heap Top: 30

    // 최소 힙
    std::priority_queue<int, std::vector<int>, std::greater<int>> min_heap;
    min_heap.push(10);
    min_heap.push(30);
    min_heap.push(20);
    min_heap.push(5);

    std::cout << "Min Heap Top: " << min_heap.top() << std::endl; // 출력: Min Heap Top: 5

    std::cout << "Max Heap elements (popping): ";
    while (!max_heap.empty()) {
        std::cout << max_heap.top() << " ";
        max_heap.pop();
    }
    std::cout << std::endl; // 출력: Max Heap elements (popping): 30 20 10 5

    return 0;
}
```

### 4. 선형 자료구조의 응용 및 알고리즘

선형 자료구조는 다양한 알고리즘의 기반이 됩니다.

#### 4.1. 배열 기반 알고리즘

*   **정렬 알고리즘:** 버블 정렬, 선택 정렬, 삽입 정렬, 퀵 정렬, 병합 정렬 등 대부분의 정렬 알고리즘은 배열을 기반으로 합니다.
*   **탐색 알고리즘:** 선형 탐색, 이진 탐색 (정렬된 배열에서) 등이 배열에서 효율적으로 작동합니다.
*   **동적 프로그래밍:** 많은 DP 문제에서 상태를 저장하기 위해 배열을 사용합니다.

#### 4.2. 연결 리스트 기반 알고리즘

*   **동적 데이터 관리:** 삽입/삭제가 빈번한 경우 (예: 음악 플레이어의 재생 목록, 텍스트 편집기의 커서 이동).
*   **그래프 알고리즘:** 인접 리스트(Adjacency List) 표현에서 각 정점의 인접 정점들을 저장하는 데 사용됩니다.
*   **메모리 관리:** 가상 메모리 페이징 시스템 등에서 사용될 수 있습니다.

#### 4.3. 스택 및 큐를 활용한 문제 해결

*   **스택:**
    *   함수 호출 스택 (재귀 구현)
    *   괄호 검사 (Balanced Parentheses)
    *   후위 표기법 계산 (Postfix Expression Evaluation)
    *   깊이 우선 탐색 (DFS) 구현
*   **큐:**
    *   너비 우선 탐색 (BFS) 구현
    *   작업 스케줄링 (CPU 스케줄링, 프린터 큐)
    *   최단 경로 찾기 (BFS 활용)

### 5. STL 사용 시 고려사항 및 팁

#### 5.1. 적절한 컨테이너 선택 기준

*   **접근 방식:**
    *   인덱스로 빠르게 접근해야 한다면: `vector`, `deque`
    *   순차 접근만 필요하고 삽입/삭제가 빈번하다면: `list`, `forward_list`
*   **삽입/삭제 위치:**
    *   끝에서만 삽입/삭제가 주로 일어난다면: `vector`
    *   양쪽 끝에서 삽입/삭제가 빈번하다면: `deque`
    *   중간에서의 삽입/삭제가 빈번하다면: `list`
*   **메모리 사용량:**
    *   메모리 효율성이 중요하다면: `vector`, `forward_list`
    *   메모리 오버헤드가 허용된다면: `list`, `deque`
*   **정렬 및 검색:**
    *   정렬된 상태를 유지하거나 빠른 검색이 필요하다면: `std::set`, `std::map` (이들은 선형 자료구조는 아니지만, 관련성이 높음)

#### 5.2. 반복자(Iterator)의 이해와 활용

STL 컨테이너의 요소에 접근하고 순회하는 핵심 도구입니다. 각 컨테이너는 특정 종류의 반복자를 제공하며, 반복자의 유효성(validity)을 이해하는 것이 중요합니다. 예를 들어, `vector`나 `deque`에서 요소를 삽입하거나 삭제하면 해당 위치나 이후의 반복자가 무효화될 수 있습니다.

#### 5.3. 메모리 관리 및 성능 최적화

*   **`reserve()`:** `vector`나 `deque`의 경우, 미리 예상되는 크기만큼 메모리를 예약(`reserve()`)하면 불필요한 재할당을 줄여 성능을 향상시킬 수 있습니다.
*   **`shrink_to_fit()`:** 사용하지 않는 여유 메모리를 해제하여 메모리 사용량을 줄일 수 있습니다.
*   **컨테이너 어댑터:** `stack`, `queue`, `priority_queue`는 내부적으로 다른 컨테이너를 사용하므로, 필요에 따라 기본 컨테이너를 변경하여 성능을 최적화할 수 있습니다. (예: `std::stack<int, std::vector<int>>`)

#### 5.4. 자주 발생하는 오류 및 디버깅

*   **반복자 무효화 (Iterator Invalidation):** 컨테이너의 구조가 변경될 때 반복자가 가리키는 요소가 유효하지 않게 되는 경우입니다. 특히 `vector`와 `deque`에서 삽입/삭제 시 주의해야 합니다.
*   **범위 오류 (Out-of-Bounds Access):** `operator[]` 사용 시 인덱스가 범위를 벗어나는 경우입니다. `at()` 메서드를 사용하면 예외 처리를 통해 안전하게 접근할 수 있습니다.
*   **`size()` vs `capacity()`:** `vector`에서 `size()`는 현재 요소의 개수, `capacity()`는 재할당 없이 저장할 수 있는 최대 요소의 개수입니다.
*   **`std::list`의 `size()`:** C++11 이전에는 `size()`가 O(n)이었으나, C++11부터 O(1)이 보장됩니다.

---
