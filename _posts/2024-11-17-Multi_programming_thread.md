---
title: 스레드 생성
tags:
  - C++
  - Multithread
use_math: true
---

스레드는 `<thread>` 헤더 파일 안에 C++ 스레드 라이브러리로 만들 수 있다.
스레드가 뭘 할 지 결정하는 방법으로 세 가지가 있다:
1. 함수 객체의 `operator()`로 표현
2. 람다 표현식 이용
3. 특정 클래스의 인스턴스로 멤버 함수 활용

### 함수 포인터로 스레드 생성
C++ 표준에서 제공되는 `std::thread` 클래스의 함수를 이용하면 원하는 만큼의 파라매터를 넘겨줄 수 있다.
다음 예제 코드를 살펴보자
```
#include<iostream>
#include<thread>

void counter(int id, int numIterations) {
	for ( int i = 0; i < numIterations; i++ ) {
		std::cout << "Counter " << id << " has value " << i << std::endl;
	}
}

int main(int argc, char** argv) {
	std::thread t1(counter, 1, 10);
	std::thread t2(counter, 2, 10);

	t1.join();
	t2.join();
	return 0;
}
```
결과
```
Counter 1 has value 0
Counter 1 has value 1
Counter 1 has value 2
Counter 1 has value 3
Counter 1 has value 4
Counter 1 has value 5
Counter Counter 21 has value  has value 60
Counter 2 has value 1
Counter 2 has value 2
Counter 2 has value 3
Counter 2 has value 4
Counter 2 has value 5
Counter 2 has value 
Counter 1 has value 7
Counter 1 has value 8
Counter 1 has value 9
6
Counter 2 has value 7
Counter 2 has value 8
Counter 2 has value 9
```
`thread`클래스 생성자는 가변 인수 템플릿이기 때문에 인수 개수를 원하는 만큼 지정할 수 있다.
첫 번째 인수는 새로 만들 스레드가 실행할 함수의 이름이다.
그 다음 인수들은 스레드 구동 시 실행할 함수에 전달할 인수이다.

`thread` 객체가 실행 가능한 상태에 있는 경우를 조인 가능(Joinable)하다고 표현한다.
이런 경우 스레드가 실행을 마치고 나서도 조인 가능한 상태를 유지한다.
조인 가능한 `thread` 객체를 제거하려면 먼저 `join()`이나 `detach()`부터 호출해야 한다.
`join()` 함수를 호출하면, 해당 스레드가 작업을 끝낼 때까지 기다린다.
`detach()`를 호출하면 OS 내부의 스레드와 분리하여 독립적으로 실행된다.
두 함수 모두 객체를 조인 불가능한 상태로 전환시킨다.
조인 가능한 `thread` 객체를 제거하면 소멸자가 `std::terminate()`를 호출해서 애플리케이션마저 종료시킨다.

위 코드의 결과는 시스템마다 그리고 같은 시스템이더라도 실행 마다 달라질 수 있다.
두 스레드가 동시에 실행하므로 시스템 코어 수와 OS의 스레드 스케쥴링 방식에 따라 달라진다.
`std::cout`의 경우 스레드에 안전하여 스레드 사이에서 데이터 경쟁이 발생하지 않지만, 결과 처럼 코드 결과가 뒤섞일 수 있다.
이 경우 동기화 기법을 적용하면 뒤섞이지 않게 만들 수 있다.

### 함수 객체를 이용해서 스레드 만들기
앞선 방법과 달리, 함수 객체를 이용하면 클래스에 멤버 변수를 추가해 원하는 방식으로 초기화해서 사용할 수 있다.
다음 코드를 살펴보자.
```
#include<iostream>
#include<thread>

class Counter {
private:
	int mId;
	int mNumIterations;
public:
	Counter(int id, int numIterations) : mId(id), mNumIterations(numIterations) { }

	void operator()() const {
		for ( int i = 0; i < mNumIterations; ++i ) {
			std::cout << "Counter " << mId << " has value " << i << std::endl;
		}
	}
};

int main(int argc, char** argv) {
	std::thread t1{Counter{1, 20}};
	Counter c(2, 12);
	std::thread t2(c);

	std::thread t3(Counter(3, 10));

	t1.join();
	t2.join();
	t3.join();
}
```
결과
```
Counter Counter 2 has value Counter 03
Counter  has value 10
Counter  has value 0
Counter 321 has value  has value  has value 1
Counter 1
Counter 31 has value 1
2
Counter Counter 2 has value 2
Counter 3 has value  has value 3
1 has value 3
Counter 1 has value 4
Counter Counter 3 has value 1 has value 2
4
5
Counter Counter 1 has value 3Counter 2 has value 3
Counter 2 has value 4
Counter 2 has value  has value 5
Counter 3 has value 6
Counter 3 has value 7
Counter 3 has value 8
Counter 3 has value 9
5
Counter 2 has value 6
Counter 2 has value 7
Counter 2 has value 8
Counter 2 has value 9
Counter 26
Counter 1 has value 7
Counter 1 has value 8
Counter 1 has value 9
Counter  has value 10
Counter 2 has value 11
1 has value 10
Counter 1 has value 11
Counter 1 has value 12
Counter 1 has value 13
Counter 1 has value 14
Counter 1 has value 15
Counter 1 has value 16
Counter 1 has value 17
Counter 1 has value 18
Counter 1 has value 19
```
`main()` 함수에서 스레드를 초기화하는 세 가지 방법이 제시되었다.
첫 번째는 유니폼 초기화로 처리하여 `Counter` 생성자에 인수를 지정해서 인스턴스를 생성하면 그 값이 중괄호로 묶인 `thread` 생성자 인수로 전달된다.
두 번째는 일반 변수처럼 네임드 인스턴스를 정의하고, 이를 `thread` 클래스의 생성자로 전달한다.
세 번째 방법은 `Counter` 인스턴스를 생성해서 이를 `thread` 클래스 생성자로 전달하는 데 중괄호가 아닌 소괄호로 묶는다.

`t1`과 `t3`의 생성을 비교해보면, 함수 객체 생성자가 매개변수를 받지 않을 때 `t3`처럼 작성하면 에러가 발생한다.
```
#include<iostream>
#include<thread>

class Counter {
private:
	int mId;
	int mNumIterations;
public:
	Counter() { }

	void operator()() const {
		for ( int i = 0; i < mNumIterations; ++i ) {
			std::cout << "Counter " << mId << " has value " << i << std::endl;
		}
	}
};

int main(int argc, char** argv) {
	std::thread t1(Counter());
	t1.join();
}
```
C++ 인터프리터는 `std::thread t1(Counter());`를 `t1` 함수의 선언문으로 해석하기 때문이다.
이 때는 유니폼 초기화를 사용하는 것이 좋다.

### 람다 표현식으로 스레드 만들기
람다 표현식을 이용하면 다음과 같이 작성할 수 있다.
```
#include<iostream>
#include<thread>

int main(int argc, char** argv) {
	int id = 1;
	int numIterations = 5;

	std::thread t1([id, numIterations] {
		for ( int i = 0; i < numIterations; i++ ) {
			std::cout << "Counter " << id << " has value " << i << std::endl;
		}
				   });

	t1.join();

}
```
결과
```
Counter 1 has value 0
Counter 1 has value 1
Counter 1 has value 2
Counter 1 has value 3
Counter 1 has value 4
```

### 멤버 함수로 스레드 만들기
스레드에서 실행할 내용을 클래스의 멤버 함수로 지정한 다음 그 멤버 함수만 실행할 수 있다.
다음 예제를 보자
```
#include<iostream>
#include<thread>

class Request {
private:
	int mId;
public:
	Request(int id) : mId(id) { }

	void process() {
		std::cout << "Processing request " << mId << std::endl;
	}
};

int main() {
	Request req(100);
	std::thread t{&Request::process, &req};
	t.join();

	return 0;
}
```
결과
```
Processing request 100
```
이 경우 똑같은 객체를 여러 스레드가 접근할 때 데이터 경쟁이 발생하지 않도록 스레드를 안전하게 작성해야 한다.
이 때 상호 배제(뮤텍스)라는 동기화 기법을 활용하면 된다.

### 스레드 로컬 저장소

C++ 표준에서는 스레드 로컬 저장소(Thread Local Storage)를 지원한다.
원하는 변수에 `thread_local`이란 키워드를 지정하면, 스레드마다 변수를 복제해서 각 스레드가 없어질 때 까지 유지한다.
각 변수는 스레드에거 한 번만 초기화된다.
예를 들어 전역 변수에 다음과 같이 정의하자.
```
int k;
thread_local int n;
```
그러면 모든 스레드가 `k`의 복제본 하나를 공유하며, 각 스레드는 자신의 고유한 `n`의 복제본을 가진다.
만약 `thread_local` 변수를 함수 스코프 안에서 선언하면, 모든 스레드가 복제본을 따로 가진다.
그리고 함수를 여러번 호출 하여도 해당 변수는 한 번만 초기화 된다.

### 스레드 취소

C++ 표준에서는 스레드를 다른 스레드에서 중단시키는 메커니즘은 제공하지 않는다.
이 때 다른 스레드를 종료시키려면 여러 스레드가 공통으로 따르는 통신 메커니즘을 제공하면 된다.
가장 간단한 방법으로 공유 변수를 활용하여, 스레드는 이 값을 주기적으로 확인하면서 중단 여부를 결정한다.
나머지 스레드는 이 공유 변수를 이용해 스레드를 간접적으로 종료시킬 수 있다.
이 때 여러 스레드가 공유 변수에 접근하기 때문에, 최소 한 스레드는 그 변수에 값을 쓸 수 있다.
따라서 공유 변수는 아토믹이나 조건 변수로 만드는 것이 좋다.

### 스레드 실행 결과 얻기

한 가지 방법은 결과를 담은 변수에 대한 포인터나 레퍼런스를 스레드로 전달해서 스레드마다 결과를 저장하는 것이다.
또 다른 방법은 함수 객체 클래스의 멤버 변수에 처리 결과를 저장했다가 나중에 스레드를 종료할 때 그 값을 가져온다.
이 방법은 반드시 `std::ref()`를 이용해서 함수 객체의 레퍼런스를 `thread` 생성자에 전달해야 한다.
또 다른 쉬운 방법은 `future`를 활용하는 것이다. `future`를 이용하면, 스레드 안에서 발생한 에러를 처리하기도 쉽다.

### 익셉션 복제와 다시 던지기

스레드에서 던진 익셉션은 스레드 안에서 처리해야 한다.
스레드에서 익셉션이 처리되지 못하면 C++ 런타임은 `std::terminate()`를 호출해서 애플리케이션을 종료시킨다.
표준 스레드 라이브러리에서는 익셉션을 처리하기 위한 함수들을 제공한다.
이 함수는 `std::exception`, `int`, `std::string` 과 커스텀 익셉션 등에도 적용된다.

- `exception_ptr current_exception() noexcept;`
`catch` 블록에서 호출하여, 처리할 익셉션을 가리키는 `exception_ptr` 객체나 복사본을 리턴한다.
익셉션이 없다면, 