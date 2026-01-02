## 1. C++ 클래스의 정의와 역사적 배경

C++ 클래스는 **객체 지향 프로그래밍**(OOP)의 핵심 요소로, 데이터와 함수를 하나의 단위로 묶어 **데이터의 은닉성**(encapsulation)과 **코드 재사용성**(reusability)을 제공합니다. C++ 클래스는 1980년대 후반에 Bjarne Stroustrup이 C 언어를 기반으로 개선한 언어로, 기존의 구조체(struct)를 확장하여 **멤버 변수와 멤버 함수를 포함**할 수 있게 했습니다.

> 📌 **클래스는 "형태"를 정의하고, 그 형식에 맞는 객체(인스턴스)를 생성하는 기반입니다.**

### 1.1 클래스 vs 구조체 (struct)

| 항목 | 구조체 (struct) | 클래스 (class) |
|------|----------------|----------------|
| 기본 접근 제어 | public (기본) | default: private |
| 상속 가능 | ❌ | ✅ |
| 생성자/소멸자 | ❌ | ✅ |
| friend 멤버 | ❌ | ✅ |
| 상수 멤버 함수 | ❌ | ✅ |

> 💡 예: `struct Point { int x, y; };` → 멤버는 모두 public  
> `class Point { private: int x, y; public: void set(int a, int b); };` → private으로 보호

---

## 2. 클래스의 구성 요소

### 2.1 멤버 변수 (Member Variables)

클래스 내부에 정의된 변수는 **멤버 변수**로, 각 인스턴스(객체)마다 별도의 공간을 할당받습니다.

```cpp
class Rectangle {
private:
    int width;
    int height;
public:
    Rectangle(int w, int h) : width(w), height(h) {}
};
```

- `private`: 외부에서 접근 불가 (멤버 함수만 접근 가능)
- `public`: 외부에서 접근 가능

> ⚠️ 멤버 변수는 **생성자 초기화 리스트**(initialization list)를 통해 초기화 가능

---

### 2.2 멤버 함수 (Member Functions)

클래스 내에 정의된 함수는 **멤버 함수**로, 객체의 행동을 제어합니다.

```cpp
class Circle {
private:
    double radius;
public:
    Circle(double r) : radius(r) {}
    double getArea() const { return 3.14159 * radius * radius; }
    void setRadius(double r) { radius = r; }
};
```

- `const` 함수는 **변수를 변경하지 않음** → 컴파일러가 안전성 보장
- `const` 함수는 `const` 멤버 함수로 선언 가능

---

## 3. 생성자 (Constructor)

### 3.1 기본 생성자

```cpp
class Person {
private:
    std::string name;
    int age;
public:
    Person() : name("Unknown"), age(0) {}
    Person(const std::string& n, int a) : name(n), age(a) {}
};
```

- 생성자는 **객체가 생성될 때 자동으로 호출**
- **복사 생성자**(copy constructor), **이동 생성자**(move constructor)도 포함

---

### 3.2 생성자 오버로딩 (Constructor Overloading)

다양한 인자 조합으로 객체를 생성할 수 있도록 여러 생성자를 정의 가능

```cpp
class Car {
public:
    Car();                    // 기본 생성자
    Car(int year, std::string model); // 인자 2개
    Car(const Car& other);    // 복사 생성자
    Car(Car&& other);         // 이동 생성자
};
```

> 💡 생성자 오버로딩은 **인스턴스화 시 유연성 제공**

---

## 4. 소멸자 (Destructor)

객체가 소멸될 때 자동으로 호출되는 함수. **메모리 누수 방지**에 중요

```cpp
class Resource {
private:
    int* data;
public:
    Resource() { data = new int[100]; }
    ~Resource() { delete[] data; } // 소멸자
};
```

- 소멸자는 **반드시 정의되어야 하는 경우가 많음** (예: 자원 관리)
- `~ClassName()` 형식

---

## 5. 접근 제어 (Access Specifiers)

| 접근 제어 | 설명 |
|----------|------|
| `private` | 클래스 내부에서만 접근 가능 (기본) |
| `protected` | 상속된 자식 클래스에서만 접근 가능 (상속 보호) |
| `public` | 외부에서 접근 가능 (기본) |

```cpp
class Base {
protected:
    int protectedData;
public:
    void set(int x) { protectedData = x; }
};
class Derived : public Base {
public:
    void access() { // protected 멤버 접근 가능
        protectedData = 100;
    }
};
```

> ✅ `protected`는 **상속을 통한 보호**를 위해 사용

---

## 6. 상속 (Inheritance)

클래스를 기반으로 다른 클래스를 **확장**하거나 **재정의**할 수 있음

### 6.1 단일 상속

```cpp
class Animal {
public:
    virtual void sound() = 0; // 추상 메서드
};

class Dog : public Animal {
public:
    void sound() override {
        std::cout << "Woof!\n";
    }
};
```

- `virtual` 키워드는 **다형성**(polymorphism)을 위해 사용
- `override`는 부모 메서드를 재정의할 때 사용

---

### 6.2 다중 상속 (Multiple Inheritance)

```cpp
class A {
public:
    void printA() { std::cout << "A\n"; }
};

class B {
public:
    void printB() { std::cout << "B\n"; }
};

class C : public A, public B {
public:
    void printAll() {
        printA();
        printB();
    }
};
```

> ⚠️ 다중 상속은 **명확한 메서드 충돌**을 유발할 수 있음 → `virtual` 키워드와 `override`를 통해 해결

---

## 7. 다형성 (Polymorphism)

동일한 인터페이스를 통해 **다른 행동을 수행**할 수 있음

```cpp
void makeSound(Animal& animal) {
    animal.sound();
}

// Dog, Cat 등이 모두 sound()를 구현하면 다형성 작동
```

- **동적 바인딩**(dynamic binding) → 런타임에 함수를 결정
- `virtual` 키워드가 필요

---

## 8. 정적 멤버 (Static Members)

클래스 전체에 공유되는 멤버

```cpp
class Counter {
private:
    static int count;  // 정적 멤버 변수
    static std::mutex mtx;
public:
    static void increment() {
        std::lock_guard<std::mutex> lock(mtx);
        count++;
    }
    static int getValue() { return count; }
};
```

- 정적 멤버는 **인스턴스 없이 접근 가능**
- `static` 키워드 사용

> ✅ 예: 게임에서 플레이어 수를 공유할 때 유용

---

## 9. 정적 함수 (Static Function)

클래스의 정적 멤버에 접근할 수 있음

```cpp
class Math {
public:
    static double add(double a, double b) {
        return a + b;
    }
};
```

- `Math::add(2, 3)`처럼 클래스 이름으로 호출 가능

---

## 10. friend 함수 및 friend 멤버

클래스 외부에서 멤버를 접근할 수 있도록 허용

```cpp
class BankAccount {
private:
    double balance;
public:
    BankAccount(double b) : balance(b) {}
    friend void printBalance(const BankAccount& acc);
};

void printBalance(const BankAccount& acc) {
    std::cout << "Balance: " << acc.balance << "\n";
}
```

> ✅ 예: 파일 입출력, 템플릿 함수 등 외부에서 접근 필요할 때

---

## 11. 생성자와 소멸자 중복 방지

### 11.1 복사 생성자 (Copy Constructor)

```cpp
class MyClass {
public:
    MyClass(const MyClass& other) {
        std::cout << "Copy constructor called\n";
    }
};
```

- 컴파일러가 자동으로 생성하지만, **복사가 원하지 않으면 명시적으로 삭제**

```cpp
MyClass(const MyClass&) = delete; // 복사 금지
```

---

### 11.2 이동 생성자 (Move Constructor)

```cpp
MyClass(MyClass&&) = default; // 이동 가능
```

- **이동은 복사보다 효율적** (예: large object, dynamic allocation)

---

## 12. 연산자 오버로딩 (Operator Overloading)

기존 연산자들을 클래스에 맞게 재정의 가능

```cpp
class Vector {
private:
    int x, y;
public:
    Vector(int a, int b) : x(a), y(b) {}
    
    Vector operator+(const Vector& other) {
        return Vector(x + other.x, y + other.y);
    }
    
    void print() {
        std::cout << "(" << x << ", " << y << ")\n";
    }
};

// 사용 예
Vector v1(1, 2), v2(3, 4);
Vector v3 = v1 + v2; // 연산자 오버로딩
```

> ✅ 유용한 경우: 벡터, 행렬, 수학적 연산

---

## 13. 상수 멤버 함수 (Const Member Functions)

```cpp
class Point {
private:
    int x, y;
public:
    void set(int a, int b) { x = a; y = b; }
    int getX() const { return x; } // const 함수
};
```

- `const` 함수는 **멤버 변수를 변경하지 않음**
- 컴파일러가 **불변성**을 보장

---

## 14. 상수 인스턴스 (const object)

```cpp
const Circle c; // c는 변경 불가
c.setRadius(10); // ❌ 컴파일 오류
```

- `const` 인스턴스는 **변경 불가능**

---

## 15. 인터페이스 설계 (Interface Design)

클래스는 **인터페이스를 정의**할 수 있음

```cpp
class Drawable {
public:
    virtual void draw() = 0; // 추상 메서드
    virtual ~Drawable() = default;
};

class Circle : public Drawable {
public:
    void draw() override {
        std::cout << "Drawing a circle\n";
    }
};
```

- **추상 클래스**(abstract class)는 인스턴스화 불가

---

## 16. 예외 처리와 클래스

```cpp
class SafeDivide {
public:
    double divide(double a, double b) {
        if (b == 0) {
            throw std::invalid_argument("Division by zero");
        }
        return a / b;
    }
};
```

- 예외는 **클래스 내부에서 처리 가능**

---

## 17. 상속과 다형성의 실생활 예제

### 17.1 게임 개발 (예: 캐릭터)

```cpp
class Character {
public:
    virtual void move() = 0;
    virtual void attack() = 0;
};

class Player : public Character {
public:
    void move() override { std::cout << "Player moving\n"; }
    void attack() override { std::cout << "Player attacking\n"; }
};

class Enemy : public Character {
public:
    void move() override { std::cout << "Enemy moving\n"; }
    void attack() override { std::cout << "Enemy attacking\n"; }
};
```

- **다형성**으로 동일한 인터페이스를 통해 다양한 행동 가능

---

## 18. C++11 이후의 클래스 기능

### 18.1 Lambda와 클래스

```cpp
class Timer {
public:
    std::function<void()> callback;
    Timer() {
        callback = []() { std::cout << "Timer expired!\n"; };
    }
};
```

- **람다 함수**를 멤버로 저장 가능

---

### 18.2 `auto`와 클래스

```cpp
auto obj = MyClass(10, 20); // 자동 타입 추론
```

- `auto`는 클래스 생성도 가능

---

## 19. 실무 적용 사례

### 19.1 데이터베이스 연결 관리

```cpp
class DatabaseConnection {
private:
    std::string host;
    std::string user;
    std::string password;
    bool connected;
public:
    DatabaseConnection(const std::string& h, const std::string& u, const std::string& p)
        : host(h), user(u), password(p), connected(false) {
        connect();
    }
    void connect() {
        if (!connected) {
            std::cout << "Connecting to " << host << "\n";
            connected = true;
        }
    }
    void disconnect() {
        connected = false;
        std::cout << "Disconnected\n";
    }
};
```

- **자원 관리, 상태 유지, 예외 처리** 가능

---

### 19.2 파일 처리 클래스

```cpp
class FileHandler {
private:
    std::string filename;
public:
    void openFile(const std::string& f) {
        filename = f;
        std::cout << "Opening file: " << filename << "\n";
    }
    void read() {
        std::ifstream in(filename);
        if (!in) {
            throw std::runtime_error("Cannot open file");
        }
        // 읽기 로직
    }
};
```

---

## 20. 실무에서의 주의사항

| 주의사항 | 설명 |
|--------|------|
| **멤버 변수는 public으로 하지 말 것** | 보안 및 유지보수 문제 |
| **생성자/소멸자에 예외 처리 포함** | 자원 누수 방지 |
| **상속 시 명확한 메서드 충돌 방지** | `virtual`, `override` 사용 |
| **정적 멤버는 공유 상태에 주의** | 동시 접근 시 경쟁 조건 발생 가능 |
| **const 함수는 변경하지 않음** | 컴파일러 최적화 및 안정성 보장 |

---

## 21. C++17 이후의 고급 기능

### 21.1 `std::optional`과 클래스

```cpp
class Result {
public:
    std::optional<int> value;
    bool is_valid() const { return value.has_value(); }
};
```

- **결과가 없을 경우** 처리 가능

---

### 21.2 `std::variant` (다형성 타입)

```cpp
class Response {
public:
    std::variant<int, std::string, std::vector<int>> data;
};
```

- **하나의 변수에 여러 타입 저장 가능**

---

## 22. C++ 클래스와 메모리 관리

- **스택 vs 힙**: 클래스 인스턴스는 스택에 저장되며, 생성/소멸은 스택에서 처리
- **힙 할당**: 멤버 변수가 `new`로 할당되면 **소멸자에서 해제**

```cpp
class LargeObject {
private:
    int* data;
public:
    LargeObject() { data = new int[1000000]; }
    ~LargeObject() { delete[] data; }
};
```

---

## 23. C++ 클래스와 템플릿

```cpp
template <typename T>
class Container {
private:
    T value;
public:
    Container(T v) : value(v) {}
    void display() const { std::cout << value << "\n"; }
};
```

- **유연한 설계**, **타입 안전**

---

## 24. C++ 클래스와 인터페이스 (Interface)

- C++는 **인터페이스를 정의할 수 없음** (추상 클래스를 사용)
- **추상 메서드**를 통해 인터페이스를 모방 가능

```cpp
class Shape {
public:
    virtual double area() = 0;
    virtual void draw() = 0;
};
```

---

## 25. 실생활 예제: 계좌 관리 시스템

```cpp
class BankAccount {
private:
    std::string accountNumber;
    double balance;
    std::string owner;
public:
    BankAccount(const std::string& acc, const std::string& owner, double init)
        : accountNumber(acc), balance(init), owner(owner) {}
    
    void deposit(double amount) {
        if (amount > 0) balance += amount;
    }
    
    void withdraw(double amount) {
        if (amount > 0 && balance >= amount) {
            balance -= amount;
        } else {
            std::cout << "Insufficient funds\n";
        }
    }
    
    double getBalance() const { return balance; }
};
```

- **실무에서 자주 사용되는 설계 패턴**

---

## 26. C++ 클래스와 디자인 패턴 (Design Patterns)

| 패턴 | 설명 |
|------|------|
| **Singleton** | 한 인스턴스만 존재 |
| **Factory** | 객체 생성을 추상화 |
| **Observer** | 상태 변화에 반응 |

```cpp
class Singleton {
private:
    static Singleton* instance;
public:
    static Singleton* getInstance() {
        if (!instance) instance = new Singleton();
        return instance;
    }
    ~Singleton() { delete instance; }
};
```

> ⚠️ `static` 멤버 함수로 인스턴스 제어 가능

---

## 27. C++ 클래스와 컴파일 시간 vs 런타임

| 시간 | 설명 |
|-----|------|
| **컴파일 시간** | 생성자, 소멸자, 정적 멤버 등 정적 생성 |
| **런타임** | 다형성, 상속, 메서드 호출 |

- `virtual` 함수는 런타임에 결정

---

## 28. C++ 클래스와 성능 최적화

- **멤버 변수 최소화** → 메모리 사용 최소화
- **const 함수는 최적화 가능** → 컴파일러가 제거 가능
- **이동 생성자 사용** → 큰 객체 처리 최적화

---

## 29. C++ 클래스와 실무 개발 가이드

### 29.1 작성 가이드

1. **명확한 이름** 사용 (예: `UserManager`, `FileProcessor`)
2. **접근 제어** 명확히 정의 (private/protected/public)
3. **생성자/소멸자** 명시적 처리
4. **예외 처리** 포함
5. **테스트 가능** (unit test 가능)

---

## 30. 결론

C++ 클래스는 **객체 지향 프로그래밍의 핵심**이며, 다음과 같은 장점이 있습니다:

- **코드 재사용** (상속)
- **보안성** (접근 제어)
- **확장성** (다형성, 인터페이스)
- **유연성** (오버로딩, 템플릿)

> ✅ **C++ 클래스는 단순한 구조체를 넘어, 복잡한 시스템 설계에 적합한 도구**입니다.

---
