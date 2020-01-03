---
layout: post
title: "Game Design Pattern"
description: ""
date: 2019-12-29 19:00:00+09:00
tags: [Game Design Pattern]
comments: true
share: true
---

[TOC]



## 좋은 소프트웨어 구조

- 새로운 작업을 할 때 코드를 거의 건드리지 않고 적당한 함수 몇 개만 호출하면 원하는 작업을 할 수 있는 코드 및 구조
- 변화가 쉬운 코드
- 작업에 들어가기 전에 기존 코드를 파악하는(알아야할 지식) 양이 적은 구조
  - 디커플링



## 추상화와 디커플링의 적절한 적용

- 유연함이 필요할지 확신이 안선다면 추상화와 디커플링을 적용하느라 시간 낭비 말라.
- 저수준의 핵심 최적화는 가능한 늦게 하라.
- 버릴 코드는 빠르게 기능을 확인하는 것이다.



## Design Pattern

### Command Pattern(명령 패턴)

- 메서드 호출을 실체화한 것
  - 실체화
    - 어떤 개념을 변수에 저장하거나 함수에 전달할 수 있도록 데이터(객체)로 바꿀 수 있다.
  - 메서드 호출을 객체화하여 전달하는 것
- 콜백을 객체지향적으로 표현한 것
- 비슷한 개념
  - 콜백
  - 일급 함수
    - 자바스크립트의 함수와 같이 함수를 할당, 전달, 반환 할 수 있는 함수
  - 함수 포인터
    - 상태값을 가지지 않지만 간단한 기능에는 사용할 수 있겠다.
  - 클로저
    - 현재 문맥(context)의 값을 저장하는 함수 객체를 간단히 만들어주므로 명령 패턴을 구현하기 이상적인 기술이지만 너무 자동화를 잘해줘서 클로저가 어떤 상태를 갖고 있는지 알아보기 어렵다.
    - 위키백과 : 컴퓨터 언어에서 클로저(Closure)는 [일급 객체 함수](https://ko.wikipedia.org/w/index.php?title=일급_객체_함수&action=edit&redlink=1)(first-class functions)의 개념을 이용하여 스코프(scope)에 묶인 변수를 바인딩 하기 위한 일종의 기술이다. 기능상으로, 클로저는 함수를 저장한 [레코드](https://ko.wikipedia.org/wiki/레코드)(record)이며, 스코프(scope)의 인수(Factor)들은 클로저가 만들어질 때 정의(define)되며, 스코프 내의 영역이 소멸(remove)되었어도 그에 대한 접근(access)은 독립된 복사본인 클로저를 통해 이루어질 수 있다.
  - 부분 적용(partial application) 함수
    - 여러 함수를 거쳐 결과를 반환하는 함수일 경우 중간까지만 계산한 값을 갖고 있는 함수를 나중에 실행하는 것.



### Flyweight Pattern(경량 패턴)

- 어떤 객체의 개수가 너무 많아서 좀 더 가볍게 만들고 싶을 때 사용



#### 경량 패턴을 사용하기 위한 데이터의 분류

- 고유 상태(intrinsic state)
  - 모든 객체의 데이터 값이 같아서 공유할 수 있는 데이터
- 외부 상태(extrinsic state)
  - 인스턴스별로 값이 다른 데이터



#### 경량 패턴 예

- 지형 데이터
  - 지형이 한정된 타입으로 구성된 경우, 타입별 지형을 만들고 전체 지형은 생성된 지형의 포인터만 갖는다.
- 경량 패턴의 객체는 여러곳에서 공유하기 때문에 변경 불가능한(immutable) 상태로 만드는게 보통이다.



### Observer Pattern(관찰자 패턴)

#### 관찰자 패턴 구성 요소

- 대상(Subject)
  - 특정 조건이 되면 관찰자 목록에 저장된 객체의 특정 메서드(onNotify())를 호출하는 객체
- 관찰자(Observer)
  - 대상 객체에 등록되어 특정 조건에 메서드(onNotify())가 호출되는 객체



#### 관찰자 패턴 사용시 주의점

- 멀티스레드, 락(lock)과 함께 사용할 때는 조심
  - 관찰자 목록의 통지 메서드를 호출할 때 락이 걸린다면 게임 전체가 교착상태에 빠질 수 있다.
- 관찰자 등록에 동적할당 컬렉션을 사용한다면 메모리 단편화가 생길 수도 있다.
  - vector같은 동적할당 컬렉션은 용량 부족 시 기존 용량의 두 배 가량의 메모리를 새로 할당받아 복사하고 기존 메모리는 해제하기 때문에 단편화가 생길 수 있다.
  - 따라서 연결 리스트로 구현하면 객체가 늘어나도 기존 용량을 해제하는 단편화가 생기지 않는다.
    - 이중 연결 리스트라면 추가/삭제가 더 간편하다.
- 관찰자 패턴은 서로 연관없는 코드 덩어리들이 서로 상호 작용하기 좋은 방법이다.
  - 하나의 기능을 구현하기 위한 코드 덩어리는 명시적으로 연결하는게 더 낫다.



#### 연결리스트 관찰자 패턴의 포인터의 포인터 예제 해석

[https://gist.github.com/parkpd/4638874487a358e27957971394d42e90](https://gist.github.com/parkpd/4638874487a358e27957971394d42e90)

```cpp
void Subject::removeObserver(Observer* observer) {
  //head변수의 포인터를 받지 않으면 head가 observer일 경우 head에 observer->next를 할당하는 코드가 필요하다.
  Observer** current = &head_;
  while (*current != NULL) {
    if (*current == observer) {
      *current = (*current)->next_;
      observer->next_ = NULL;
      return;
    }
    current = &(*current)->next_;
  }
}) 
```



#### 요즘의 관찰자 패턴

- 언어 자체적으로 지원하는게 많다.
  - C# : event
  - Java : EventListener
- 클로저가 있는 언어는 클로저로 구현하는 경우가 많다.



#### 미래의 관찰자 패턴

- UI같이 성능에 덜 민감하고 데이터에 따른 갱신이 필요한 분야에서는 데이터 바인딩 방식이 대세가 될 것이다.



### Prototype Pattern(프로토타입 패턴)

- 객체를 생성할 때 클라스가 아닌 인스턴스로부터 생성하는 방식



#### CPP에서 프로토타입

- cpp에서는 clone함수를 만들어 객체의 생태를 복사하는 형식으로 만들어야하는데 이는 코드 양도 많고 요즘 일반적인 방법은 아니다. 
- 다음과 같이 클래스를 사용하는 방식이 프로토타입을 구현한 것은 아니지만 비슷하게 사용할 수 있는 방법이다.
  - cpp에서는 클래스가 일급 자료형이 이니므로 클래스를 함수의 매개변수로 전달하지 못하기 때문에 이와 같은 방법이 필요하다.
  - 자바스크립트, 파이썬, 루비 등은 클래스가 일급 자료형이다.



##### 몬스터를 스폰하는 프로토타입 예제(함수포인터 사용)

- 몬스터를 생성하는 함수 정의
- 몬스터 생성 함수를 저장하는 스폰 클래스 정의

```cpp
//Ghost는 Monster를 상속한다.
Monster* spawnGhost(){
	return new Ghost();
}

typedef Monster* (*SpawnCallback)(); //Monster반환 함수 포인터

class Spawner{
    public:
    	Spawner(SpawnCallback spawn) spawn_(spawn){}
    	Monster* spawnMonster(){return spawn_();}
    private:
    	SpawnCallback spawn_;
}
//스폰 객체 생성
Spawner* ghostSpawner = new Spawner(spawnGhost);
//몬스터 스폰
ghostSpawner.spawnMonster();
```



##### 몬스터를 스폰하는 프로토타입 예제(템플릿 사용)

- 스폰 클래스 정의
- 템플릿 타입 매개변수로 몬스트 클래스 전달

```cpp
//Spawner 클래스를 따로 만드는 이유는 몬스터를 스폰하는 코드에 매번 템플릿 매개변수로 Monster 관련 클래스를 넣지 않기 위함
class Spawner {
    public:
    	virtual ~Spawner(){}
    	virtual Monster* spawnMonster() = 0;
};

template <class T>
class SpawnerFor : public Spawner{
    public:
    	virtual Monster* spawnMonster(){
            return new T();
        }
}

// 스폰 객체 생성, Ghost는 Monster의 유도객체
Spawner* ghostSpawner = new SpawnerFor<Ghost>();
```



#### 프로토타입 언어 패러다임

- 객체를 원형으로 하여 복제의 과정을 통하여 객체의 동작 방식을 다시 사용할 수 있는 프로그래밍 방식
- 프로토타입 최고 구현 언어는 셀프이다.



##### 자바스크립트에서의 프로토타입

- 언어적으로 프로토타입을 기본으로 제작되었지만 객체의 복제를 지원하지 않고 클래스 기반의 프로그래밍 방식을 사용하고 있다.



##### 자바스크립트 객체 생성 방식

- new로 인해 빈 객체가 생성되고 생성자 함수의 this로 바인딩된다.
- 생성된 객체의 `__proto__` 필드에 생성자 함수의 prototype을 저장한다.
- 생성자 함수의 반환값으로 새로운 객체를 반환한다.

```js
//클래스 정의(JS에서 클래스는 생성자 함수의 정의와 같다)
function A(b){
	this.b = b; //b라는 필트를 추가한다.
}
//A의 prototype에 fn 함수를 추가한다. new A(1) 이후에 해도 상관없다.
A.prototype.fn = function(){
    console.log(this.b);
};

var a = new A(1);
a.__proto__; // a에 필드가 없을 때 위임하는 객체, A.prototype
a.fn(); // 1, a객체에 fn필드가 없기 때문에 위임 객체는 A.prototype객체에 fn이 있는지 찾아 호출한다.

```



#### 데이터 모델링을 위한 프로토타입

- 데이터에 프로토타입 언어와 같이 위임을 설정할 수 있다면 이를 활용하여 데이터의 중복을 제거할 수 있다.
- Json과 같은 데이터 구조에서 프로토타입을 대른 데이터로 지정한다면 공통되는 필드를 모두 지정하지 않아도 프로토타입의 위임 기능으로 찾아올 수 있다.

```js
var a = {
	name:"abc",
};
var b = {
	hp:10
};
b.__proto__ = a;//(참고로 a는 함수가 아니므로 protytype필드가 없다)
console.log(b.name); // abc
```



### Singleton Pattern(싱글턴 패턴)

- 오직 한 개의 클래스 인스턴스만을 갖도록 보장하고, 이에 대한 전역적인 접근점을 제공



#### 싱글턴을 사용하는 이유

- 한 번도 사용하지 않는다면 아예 인스턴스를 생성하지 않는다.
- 런타임에 초기화된다.
  - 싱글턴 대신 정적 멤버 변수를 사용할 수 있지만 정적 멤버 변수는 다음과 같은 단점이 있다.
    - 정적 멤버 변수는 자동 초기화된다.
      - 따라서 프로그램 실행 이후에 알 수 있는 정보를 활용할 수 없다.
      - 초기화 순서를 컴파일러에서 보장해주지 않기 때문에 다른 정적 변수에 안전하게 의존할 수 없다.
    - 싱글턴은 최대한 늦게 초기화 된다.
- 싱글턴을 상속할 수 있다.



#### 싱글턴이 문제인 이유

- 싱글턴은 사실 전역 변수와 같다.
  - 전역 변수는 코드를 이해하기 어렵게 한다.
    - 정적 변수의 값을 바꾸는 곳을 찾기가 쉽지 않다.
  - 전역 변수는 커플링을 조장한다.
  - 전역 변수는 멀티스레딩 같은 동시성 프로그래밍에 맞지 않다.
- 싱글턴은 문제가 하나일 때도 두 가지 문제를 풀려 한다.
  - 오직 한 개의 인스턴스만 필요한 경우
  - 전역 접근이 필요한 경우
- 게으른 초기화는 제어할 수가 없다.
  - 인스턴스가 사용되는 시점에 초기화 된다면 성능이 중요한 곳에서 느려질 수 있다.
  - 게이른 초기화는 메모리 단편화를 불러올 수 있다.
    - 이를 해결하기 위해 싱글턴 멤버 변수를 포인터가 아닌 변수로 만들어 main 함수가 불리기 전에 초기화가 되도록 강제할 수 있다.
      - 이는 또 다른 단점을 불러온다.
        - 다형성을 활용할 수 없다.
        - 인스턴스가 필요없어도 메모리를 해제할 수 없다.
      - 정적 멤버로 해결 할 수 있다면 instance() 함수 대신 정적 멤버를 사용하는게 더 명확한 코드이다.



#### 싱글턴의 대안

- 싱글턴이 단순히 다른 클래스의 인스턴스의 관리용이라면 기능을 클래스로 옮긴다.
- 인스턴스가 하나만 필요하다면 생성자에 단언문(assert) 등으로 이미 생성된 인스턴스가 있는지 확인한다. 
- 싱글턴은 인스턴스에 쉽게 접근할 수 있기 때문에 널리 쓰인다. 이를 해결하여 싱글턴 사용을 줄일 수 있다.
  - 넘겨주기, 의존성 주입(dependency injection)
    - 필요로 하는 의존 객체를 전역이 아닌 매개변수로 받아서 사용한다.
  - 상위 클래스로부터 얻기
  - 이미 전역인 객체로부터 얻기
  - 서비스 중개자로부터 얻기
    - 전역 접근을 제공하는 용도로만 사용하는 클래스를 따로 정의하여 전역 인스턴스를 제공한다.
- 싱글턴을 사용하지 않고도 게임을 만들 수 있다.
  - 인스턴스를 하나로 제한할 경우 
    - 정적 클래스를 사용
    - 생성자에 정적 플래그를 둬서 런타임에 인스턴스 개수 검사
- 여튼 싱글턴은 전역적으로 데이터를 변경시킬 수 있기 때문에 최소화해야한다.



### State Pattern(상태 패턴)

- 상태 패턴의 목표
  - 같은 상태에 대한 모든 동작과 데이터를 클래스 하나에 캡슐화하는 것



#### FSM(Finite State Machine - 유한 상태 기계)

- 한 번에 하나의 상태만 갖는다.
- 조건에 따라 다른 상태로 전이(transition)될 수 있다.



##### FSM을 머드 게임의 맵에 비유

- 각 방은 상태들
- 주인공이 있는 방은 현재 상태
- 각 방의 출구는 전이
- 이동 명령은 입력



##### FSM 구현

- 상태 객체를 갖는 객체
  - 상태 객체에 현재 객체의 업데이트를 맡긴다.
- 상태 객체
  - 상태 전이 함수를 갖는다.
    - 매개변수로 받은 값으로 전이된 상태 객체를 반환한다.
  - 상태가 전이됐을 때 초기화 및 정리가 필요할 수 있으므로 입장, 퇴장 함수를 갖는다.

```cpp
class Hero{
private:
	HeroState* state_;
}
void Hero::handleInput(Input input) {
    //상태객체가 전이된 상태를 반환한다
	HeroState* state = state_->handleInput(*this, input);
    if(state != nullptr) {
        //현재 상태객체 교체하고 Hero 객체를 갱신한다.
        state_->exit(*this);
        delete state_;
        //새로운 상태 할당
        state_ = state;
        //새로운 상태로 입장
        state_->enter(*this);
    }
    //상태에 따라 갱신
    state_->update(*this);
}

class HeroState{
public:
    HeroState* handleInput(Hero, Input) = 0;
    void enter(Hero) = 0;
    void exit(Hero) = 0;
    void update(Hero) = 0;
}
class HeroStateStanding : public HeroState {
    HeroState* handleInput(Hero &hero, Input input) {
        //현재 상태에서 전이될 수 있는 상태중에 조건에 맞는 상태를 반환한다.
        if(input == PRESS_DOWN){
            return new HeroStateDucking();
        }
    }
    void enter(Hero &hero) {
        //현재 상태에 맞춰 Hero 초기화
    }
    void exit(Hero &hero) {
        //현재 상태의 종료를 위한 정리
    }
    void update(Hero &hero) {
        //hero 갱신
    }
}
class HeroStateDucking : public HeroState { ... }

// ----- 상태 객체를 정적 변수로 만들어 사용 ----- //
// 상태 객체가 상태(멤버변수)를 갖지 않는 경우 
// 함수는 모두 공통으로 사용하기 때문에 정적 상태 변수로 미리 만들어 놓고 사용
class HeroState{
public:
    static HeroStateStanding standing;
    static HeroStateDucking ducking;
    ...
}
class HeroStateStanding : public HeroState {
    HeroState* handleInput(Hero &hero, Input input) {
        //현재 상태에서 전이될 수 있는 상태중에 조건에 맞는 상태를 반환한다.
        if(input == PRESS_DOWN){
            return &HeroState::standing;
        }
    }
    ...
}
```



##### FSM의 단점과 해결

###### 병행 상태 기계

- 문제
  - 상태가 두가지 이상 조합될 경우 각각의 상태를 조합한 새로운 상태를 만들어야한다.
    - n개의 상태와 m개의 상태가 조합되는 n*m개의 상태가 생긴다.
    - 상태 코드가 중복된다.
- 해결
  - 상태들이 전혀 연관이 없다면 다음과 같이 한다.
    - 각각의 상태를 나눈다.
    - 상태가 각각 전이되도록 한다.
  - 상태들이 연관이 있다면 다른 상태 기계의 상태를 알아야하므로 코드가 지저분해진다.



###### 계층형 상태 기계

- 문제 
  - a, b, c 상태 모두 d 상태로 전이 될 수 있는 경우 a, b, c 모든 상태에 전이되는 조건 코드가 중복된다.
- 해결
  - 상태 기계를 상속관계로 만들어 같은 전이가 필요한 상태들이 상속받도록 한다.
  - 서기, 걷기, 달리기, 미끄러지기 등에서 모두 점프로 전이되는 경우
    - 점프로 전이되는 코드를 상위 상태 기계 클래스에 작성하고
    - 서기, 걷기, 달리기, 미끄러지기 상태 기계 클래스가 상속 받도록 한다.



##### 푸시다운 오토마타(push-down Automata)

- 문제
  - 계층형 상태 기계와 같이 스택을 구현한 경우 이력이 없다는 문제가 있다.
  - 이전 상태에 대한 이력이 없기 때문에 이전으로 전이할 수 없다.
- 해결
  - 상태를 스택으로 관리한다.
    - 새로운 상태를 스택에 넣는다.(push)
    - 최상위 상태를 스택에서 뺀다.(pop)
    - 상태가 종료된 경우 이전 상태로 돌아갈 수 있다.



##### 푸시다운 오토마타를 이해하기 위한 개념

###### 오토마타(Automata)

- 기계 내부의 구성이나 동작에 대산 세부 사항이 무시되고 입력과 출력에 대한 사항만이 명시되는 추상적인 기계
- 계산 능령이 있는 추상 기계와 그 기계를 이용해서 풀 수 있는 문제들에 대한 학문적 접근
- 동작 방식
  - 오토마타는 유한한 내부상태를 가지며 무한한 저장공간을 가질 수도 있다.
  - 입력은 유한한 문자열이고 한번에 하나의 입력문자을 읽을 수 있다.
    - 읽은 문자와 현재의 내부상태, 그리고 저장공간에 적힌 값에 따라서 다음의 내부상태가 바뀐다.

###### 푸시다운 오토마타

- 내부상태 이외에 스택으로 된 저장공간을 갖는 오토마타
- 입력 문자열이 주어지면 이것을 하나씩 읽으면서 내부 상태를 바꿔나간다. 동시에 스택 맨 위의 적힌 내용을 읽고 바꾸거나 지우거나 새로 쓸 수 있다.



##### FSM이 유용한 경우

- 내부 상태에 따라 객체 동작이 바뀔 때
- 이런 상태가 그다지 많지 않은 선택지로 분명하게 구분될 수 있을 때
- 객체가 입력이나 이벤트에 따라 반응할 때



### Strategy Pattern(전략 패턴)

- 객체가 할 수 있는 행위를 개별 클래스(전략)로 만들어 인스턴스화 하여 위임하고, 동적으로 행위의 수정이 필요한 경우 다른 행동을하는 인스턴스(전략)로 교체한다.
- 컴포넌트 패턴과 유사하다.
  - 전략 패턴은 내부 상태가 없는 경우가 대부분이고
  - 컴포넌트 패턴은 상태를 갖는 경우가 많다.
  - 하지만 엄밀하게 나뉘지는 않는다.





## Sequencing Patterns(순서 패턴)

### Double Buffer Pattern(이중 버퍼 패턴)

#### 의도

- 여러 순차 작업의 결과를 한 번에 보여준다.
- 컴퓨터 그래픽스의 더블 버퍼링을 생각하면 된다.



#### 구조

- 버퍼 클래스이 버퍼는 점차적으로 수정되지만 밖에서는 한 번에 바뀌는 것처럼 보인다.
- 이를 위해 버퍼 클래스는 현재 버퍼와 다음 버퍼, 두 개의 버퍼를 갖는다.
- 정보를 읽을 때는 현재 버퍼에 접근하고 정보를 쓸 때는 다음 버퍼에 접근한다.
- 다음 버퍼의 변경이 완료되면 현재 버퍼와 다음 버퍼를 교체한다.



#### 사용하는 곳

- 순차적으로 변경해야하는 곳
  - 이 생태는 변경 도중에도 접근 가능해야 한다.
    - 바깥 코드에서는 작업중인 상태에 접근할 수 없어야 한다.
      - 상태에 값을 쓰는 도중에도 기다리지 않고 바로 접근할 수 있어야 한다.
- 어떤  상태를 변경하는 코드가, 동시에 지금 변경하려는 상태를 읽는 경우
  - 물리나 인공지능 같이 객체가 서로 상호작용할 때 이런 경우가 많다.
    - 모든 객체의 상태 변수는 현재, 다음 두 개로 나뉜다.
    - 모든 객체의 상태 업데이트 시 다음 상태 변수에 기록한다.
    - 기록된 다음 생태값을 현재 상태값에 기록한다.
    - 변경된 사항은 다음 프레임에 적용된다. 

```cpp
//의사 코드
void updateAll(){
	for objs.update();//상태를 업데이트 한다. 다음 버퍼에 기록된다.
	for objs.swap();//상태를 변경한다. 현재 버퍼에 다음 버퍼의 값을 기록한다.(포인터를 교체하거나 값을 복사한다)
}
```



#### 주의사항

- 교체 연산 자체에 시간이 걸린다
  - 교체 연산은 원자적이어야 하고 교체 중 두 버퍼 모두 접근할 수 없어야한다.
  - 버퍼에 값을 쓰는 시간보다 교체 시간이 더 오래 걸린다면 버퍼 패턴은 아무런 도움이 안된다.
- 버퍼가 두 개 필요하다
  - 필요한 메모리가 두 배이다.
  - 메모리가 부족하다면 이중 버퍼 패턴을 포기하고 상태 변경 시 밖에서 접근하지 못하게 할 방법을 찾아야 한다.



#### 디자인 결정 시 고려사항

##### 버퍼를 어떻게 교체할 것인가?

- 버퍼 포인터나 레퍼런스를 교체
  - 버퍼 메모리 두 개를 번갈아 가며 현재 버퍼 메모리로 지정한다.
  - 특징
    - 빠르다
    - 버퍼 코드 밖에서는 버퍼 메모리를 포인터로 저장할 수 없다는 한계가 있다
    - 버퍼에 남아 있는 데이터는 바로 이전 프레임 데이터가 아닌 2프레임 전 데이터이다.
      - 일반적으로 그리기 전에 버퍼를 정리하는 경우는 별 문제가 안된다.
      - 버퍼에 남은 데이터를 재사용할 경우 문제가 된다.
        - 모션 블러 효과를 주기 위해서 현재 프레임 이미지에 이전 프레임 값을 살작 섞어서 이미지를 뭉개기 때문에 문제가 될 수 있다.
- 버퍼끼리 데이터를 복사
  - 다음 버퍼에 데이터를 기록하고 현재 버퍼에 데이터를 복사한다.
  - 특징
    - 다음 버퍼에는 딱 한 프레임 전 데이터가 들어 있다.
      - 이전 버퍼에서 좀 더 최신 데이터를 얻을 수 있다는 점에서는 두 버퍼를 교체하는 방식보다 좋다.
    - 교체 시간이 더 걸린다.
      - 교체를 하려면 전체 버퍼를 다 복사해야 한다.
      - 버퍼가 크다면 시간이 오래걸리고 이 시간동안 버퍼 모두 읽기 쓰기가 불가능하기 대문에 제약이 크다.



##### 얼마나 정밀하게 버퍼링할 것인가?

- 버퍼가  한 덩어리라면
  - 간단히 교체 가능
  - 포인터로 버퍼를 가리키고 있다면 버퍼의 크기와 상관없이 간단히 교체 가능
- 여러 객체가 각종 데이터를 들고 있다면
  - 교체가 더 느리다.
    - 전체 객체 컬렉션을 순회하면서 교체하라고 알려줘야 한다.
    - 만약 객체 개별적으로 현재 버퍼와 다음 버퍼의 교체를 관리할 필요가 없다면 정적 변수(함수)로 현재와 다음 버퍼를 지정하는 값을 변경해 줄 수 있다.
      - 모든 객체가 현재 버퍼와 다음 버퍼의 교체를 동일하게 한다면 정적 함수로 관리할 수 있다.
        - 이런게 얼마나 있을까?



### Game Loop Pattern(게임 루프 패턴)

#### 의도

- 게임 시간 진행을 유저 입력, 프로세서 속도와 디커플링한다.



#### 동기

- 일반 애플리케이션과 같이 사용자의 반응에 응답하는 프로그램은 사용자의 입력이 있을 때까지 대기한다.
- 게임도 마찮가지지만 다른 점은 사용자가 입력하지 않아도 마냥 대기하지 않고 루프를 실행한다.

```cpp
//게임 루프
while(true){
	processInput();//이전 호출 이후 들어온 사용자 입력 처리
	update();//게임 시뮬레이션을 한 단계 실행(AI, 물리 순으로 실행)
	render();//게임 화면 그리기
}
```



#### 게임에서의 시간

- 초당 프레임을 제어하는 코드가 없다면 한 프레임당  시간은 다음과 같은 요소로 결정된다.
  - 한 프레임에 얼마나 많은 작업을 하는가
  - 코드가 실행되는 플랫폼의 속도
- 현재는 게임이 실행되는 하드웨어를 한정할 수 없는 경우가 더 많기 때문에 어떤 하드웨어에서라도 일정한 속도로 실행될 수 있도록 하는 것이 게임 루프의 핵심 업무다.



#### 언제 쓸 것인가?

- 게임이라면 게임 루프는 무조건 사용된다.



#### 주의사항

##### 플랫폼의 이벤트 루프에 맞춰야 할 수도 있다

- 윈도우에서는 루프안에서 GetMessage()대신 PeekMessage()를 호출해 OS의 이벤트 루프에서 벗어날 수 있다.
- 웹 브라우저에서는 이벤트 루프를 제어하기 힘드므로 웹 브라우저에 맞워야 할 수도 있다.



### Update Method Pattern(업데이트 메서드 패턴)



## Behavioral Patterns(행동 패턴)

### Bytecode Pattern(바이트코드 패턴)

- 데이터와 더불어 행동까지 지정할 수 있는 외부 데이터
- 프로그램 실행 중에 해석되는 인터프리터 언어와 비슷한 개념



### Subclass Sandbox Pattern(하위 클래스 샌드박스 패턴)

- 행동의 기본 단위를 상위 클래스에 작성하고 하위 클래스에서는 이 행동들을 조합하여 고유 행동을 만든다.
- 하위 클래스에서 상위 클래스 메서드를 조합하여 고유 메서드를 만들 때 이 메서드를 샌드박스 메서드라 한다.



#### 의도

- 상위 클래스가 제공하는 기능들을 통해서 하위 클래스에서 행동을 정의한다.



#### 동기





### Type Object Pattern(타입 객체 패턴)

- 여러 객체끼리 데이터와 동작을 공유하려는 것
- 공통되는 데이터와 동작을 다른 클래스로 만들어 위임하고 포함시킨다.
  - 보통 불변 데이터를 주로 위임한다
  - 상태 패턴에서는 객체의 현재 상태가 어떤지를 나타내는 임시  데이터를 주로 위임한다.





## Decoupling Pattern(디커플링 패턴)

### Component Pattern(컴포넌트 패턴)

- 개별 행위를 책임질 클래스(컴포넌트)를 만들고 이들을 조합하여 객체의 행동을 표현한다.
- 행위의 주체가 되는 클래스는 컴포넌트들을 관리하고 컴포넌트들을 사용하여 행동한다.

#### 의도

- 한 개체가 여러 분야를 서로 커플링 없이 다룰 수 있게 한다.



### Event Queue Pattern(이벤트 큐 패턴)

#### Intent

- 메시지나 이벤트를 보내는 시점과 처리하는 시점을 디커플링한다.



#### Motivation

- Observer Pattern, Command Pattern과 같은 동기적 이벤트 호출(즉시성)의 문제점
  - 처리가 완료될 때까지 블록된다.
    - 사운드 재생과 같이 디스크에서 로딩하는 경우
  - 요청을 모아서 처리할 수 없다.
  - 요청이 원치 않는 스레드에서 처리된다.
    - 요청을 받아 처리하는 객체가 요청을 처리하기 적당한 시기가 아닐 수 있다.



#### Concept Of Event Queue Pattern

- 큐에는 요청이나 알림을 들어온 순서대로 저장
- 요청을 큐에 넣은 뒤에 결과를 기다리지 않고 리턴(비동기)
- 요청을 처리하는 곳에서 큐에 들어 있는 요청을 나중에 처리
  - 직접 처리하거나 다른 곳으로 보내질 수 있다.
- 코드뿐만 아니라 시간 측면에서도 디커플링 된다.



#### When to Use It

- 메시지를 보내는 시점과 받는 시점을 분리하고 싶을 때 Event Queue Pattern을 사용한다.
  - 메시지를 보내는 곳과 받는 곳만 분리하고 싶으면 Observer Pattern, Command Pattern을 사용하면 더 간단하게 구현할 수 있다.
- 메시지를 보내는 쪽에서 응답을 받아야한다면 큐를 쓰는게 적합하지 않다.



#### Keep in Mind

- Event Queue는 복잡하고 게임 구조에 전반적인 영향을 미치기 때문에 어떻게 사용할지, 정말 쓸 것인지를 잘 생각해야한다.
- 중앙 이벤트 큐는 전역변수와 같다.
  - 따라서 전역적 접근이 가능하기 때문에 문제가 생기기 쉽다.
- 월드 상태는 언제든 바뀔 수 있다.
  - 이벤트를 받았을 때는 현재 월드 상태가 이벤트가 만들어진 당시 상태와는 다를 수 있기 때문에 이런 비동기적 이벤트는 동기적 이벤트보다 데이터가 많이 필요하다.
- 피드백 루프에 빠질 수 있다.
  - 두 객체가 서로 이벤트를 주고받는 순환이 생기지 않도록 주의한다.
    - 동기적 이벤트는 스택 오버플로 크래시가 나기 때문에 금방 찾을 수 있지만 이벤트 큐 시스템은 문제를 감지하고 찾기가 쉽지 않다.



#### 예제

- 사운드 출력 객체에 사운드 출력을 요청(이벤트 발생)
- 사웅드 출력 객체는 일단 큐에 넣고 다음 처리 주기가 올 때까지 대기했다가 처리한다.
- 기본 배열을 큐로 사용하고 원형 버퍼로 구현한다.



##### A ring buffer 원형 버퍼

- head는 큐에서 요청을 읽을 위치
- tail은 큐에 새로운 요청이 들어갈 자리
  - 마지막 요청의 다음 칸이다.
- 버퍼가 가득차면 Doubling으로 배열 크기를 늘린다.
  - 배열이 늘어날 때 데이터를 복사해야하는 단점이 있지만 Amortized Analysis에 의하면 큐에 데이터를 넣는 작업은 평균적으로 상수 시간(O(1))에 가능하다.



##### Aggregating requests 요청 취합하기

- 대기 중인 요청을 확인할 수 있기 때문에 같은 요청이 있다면 병합한다.
- 큐에 넣기 전에 병합한다.
  - 병합을 위해 같은 요청이 있는지 확인하는 비용을 줄이려면 다른 자료형을 사용한다.
    - id를 키로 하는 해시 테이블에 저장한다면 상수 시간에 중복을 검출할 수 있다.
      - 근데 이렇게 하면 해시 테이블은 큐와 같이 엘리먼트 순서를 정할 수 없기 때문에 큐와 해시 테이블 두 개를 유지해야할듯.



##### Source Code

```cpp
class Audio{
public:
	void playSound(soundData){
        //같은 요청이 있는지 확인해서 무시할 수 있다
        for(i=head_; i!=tail; i=(i+1)%MAX_PENDING){
            if(pending_[i] == soundData) return;
        }
        pending_[tail_] = soundData;//요청을 tail_위치에 추가
        tail_ = (tail_+1) % MAX_PENDING;//끝이면 처음으로 보낸다
	}
	void update(){
        if(head_ == tail_) return;
        startSound(pending_[head_]);//head_ 위치의 요청 처리
        head_ = (head_+1) % MAX_PENDING;//끝이면 처음으로 보낸다
	}
	static const int MAX_PENDING = 16;
	static SoundData pending_[MAX_PENDING];//큐, 보류된 요청
	static int head_;
	static int tail_;
}
```



#### 멀티스레드에서는?

- Event Queue 패턴에는 이미 다음과 같은 구조가 있다.
  - 요청 코드와 처리 코드가 분리되어 있다.
  - 양쪽 코드 사이에 Marshalling을 제공하기 위한 큐가 있다.
  - 큐는 나머지 코드로부터 캡슐화되어 있다.
- 따라서 요청 코드와 처리 코드를 스레드 안전하게 만들면 된다.



#### Design Decisions

##### What goes in the queue? 큐에 무엇을 넣을 것인가?

###### If you queue events 큐에 이벤트를 넣는 경우

- 이벤트는 이미 발생한 사건을 표현한다.

- 복수 개의 리스너를 지원해야 할 때도 많다.

  - 이미 발생한 일이므로 받아서 처리할 곳이 많을 수 있다.

- 큐의 범위가 더 넓은 편이다.

  - 이벤트를 원하는 누구에게든지 전파하는 용도이기 때문에 리스너 등록기 쉽도록 전역적으로 노출한다.



###### If you queue messages 큐에 메시지를 넣는 경우

  - 메시지는 나중에 실행했으면 하는 행동을 표현한다.
    - 사운드 틀기 등
  - 서비스에 비동기적으로 API를 호출하는 것과 같다.
  - 대부분은 리스너가 하나이다.
      - 비동기적 API 호출과 같기 때문에 행동할 객체가 이미 정해져있다.



##### Who can read from the queue? 누가 큐를 읽는가?

###### A single-cast queue 싱글캐스트 큐

- 큐가 어떤 클래스의 API 일부일 때 적합
  - 호출하는 쪽에서는 공개된 API만 보인다.
- 큐는 밖에서는 보이지 않는 내부 구현이 된다.
- 큐가 더 캡슐화되어 있다.
- 리스너가 하나이기 때문에 리스너간 경쟁을 고민할 필요가 없다.



###### A broadcast queue 브로드캐스트 큐

- 대부분의 이벤트 시스템이 브로드캐스트 큐이다.
  - 여러 개의 리스너가 있으며 리스너 모두에게 이벤트를 알려준다.
- 이벤트가 무시될 수 있다.
  - 리스너가 없다면 이벤트는 무시된다.
- 이벤트 필터링이 필요할 수 있다.
  - 리스너가 특정 이벤트만 받도록 이벤트 집합을 조절한다.



###### A work queue 작업 큐

- 브로드캐스트와 비슷하게 리스너가 여러 개 있다.
- 차이점은 이벤트가 리스너 한곳으로만 전달된다.
  - 스레드 풀에 작업을 나눠줘야하는 경우 일반적으로 사용된다.
- 작업을 분배해야한다.
  - Round-robin, Random, 그 외 복잡한 우선순위 시스템 등



##### Who can write to the queue? 누가 큐에 값을 넣는가?

###### With one writer 넣는 측이 하나라면

- 동기형 Observer Pattern에 가깝다.
  - 특정 객체만 이벤트를 만들 수 있고, 나머지는 이벤트를 받을 수만 있다.
- 큐에 값을 추가할 수 있는 객체가 하나이므로 누가 이벤트를 보내는지 안다.
- 보통 리스너가 여러 개다.



###### With multiple writers 넣는 측이 여러 개라면

- 예제의 오디오 엔진이 이 구조이다.
  - 코드 어디에서나 큐에 요청을 넣을 수 있다.
- 이벤트 순환을 주의해야 한다.
  - 이벤트 처리도중 큐에 이벤트가 들어올 수 있다.
    - 피드백 루프가 생길 수 있다.
- 이벤트를 보낸 객체의 레퍼런스를 이벤트에 추가 해야 할 수도 있다.
  - 이벤트는 누구나 보내기 때문에 리스너는 누가 보냈는지 알 수 없다.



##### What is the lifetime of the objects in the queue? 큐에 들어간 객체의 생명주기는 어떻게 관라할 것인가?

###### Pass ownership 소유권을 전달한다

- 메시지가 큐에 들어가면 메시지의 소유권을 큐가 가져간다
  - C++의 unique_ptr<T>와 비슷하다



###### Share ownership 소유권을 공유한다

- 메시지를 보낸 객체와 큐에서 메시지의 참조를 가질 수 있다.
  - shared_ptr<T>와 비슷
  - GC의 대상이된다.



###### The queue owns it 큐가 소유권을 가진다.

- 보내는 쪽에서 큐의 레퍼런스를 요청하여 작성하고 받는 쪽에서 참조하여 행동한다.
- 메시지의 삭제는 큐가 한다.



#### See Also 참고자료

- Event Queue는 Observer Pattern의 비동기형이다.
- 이벤트 큐를 메시지 큐라고도 부르지만 메시지 큐는 좀 더 고수준의 구조를 부를 때 사용된다.
  - 여러 어플끼리 통신 또는 대규모 분산처리 시스템을 가리키는 용도
  - publish/subscribe 또는 pubsub이라 부르기도 한다.







## 용어

- Queuing(큐잉)
  - 큐에 넣는것?
- Tearing(테어링)
  - tear : 찢다
  - 비디오 버퍼에 프로그램이 화면을 다 그리기 전에 비디오 드라이버가 버퍼를 읽어 화면에 출력하면 이전 프레임과 현재 프레임이 동시에 그려지며 화면이 어긋나 찢어진듯이 보이는 현상
- Atomic(원자적)
  - 더 이상 나누어 질 수 없는 하나의 행위
  - 수행 도중 중단될 수 없는 하나의 동작 단위
  - 예
    - 프로세스가 명령어(instruction)를 실행 중이라면 어떤 인터럽트가 발생하더라도 명령어를 수행을 완료한 후 인터럽트를 처리한다.
    - 데이터베이스의 트랜잭션은 본래 원자성이 없는 명령어들을 묶어 원자성을 가진 실행 단위로 만든 것
- Marshalling(마샬링)
  - 한 객체의 메모리에서의 표현 방식을 저장 또는 전송에 적합한 다른 데이터 형식으로 변환하는 과정
  - 데이터를 컴퓨터 프로그램의 서로 다른 부분 간에 혹은 한 프로그램에서 다른 프로그램으로 이동해야 할 때도 사용
  - Serialization(직렬화)과 유사
  - 반대 개념은 Unmarshalling 혹은 Demarshalling이라하고 Deserialization과 유사하다.
- Serialization(직렬화)
  - 오브젝트의 상태를 오브젝트의 사본으로 다시 변환할 수 있는 바이트 스트림으로 변환하는 것









## 영어

- intrinsic *[intrínsik]*
  - 본질적인, 고유한, 내재한
- extrinsic *[ikstrínsik]*
  - 비본질적인, 고유의 것이 아닌, 외부(로부터)의
- heroine *[hérouin]*
  - 여주인공
- interpret
  - ~을 해석하다.
- Breed *[briːd]*
  - 품종
- amortize *[ǽmərtàiz]*
  - 분할 상환하다
- pending *[péndiŋ]*
  - 현안의, 남아있는, 계류중인, 미결, 당면한
- aggregate *[ǽgrigət]*
  - 잡합한, 집합체, 모으다.



# 참고

- [서적] 게임 프로그래밍 패턴 / 로버트 나이트롬, 박일
  - http://gameprogrammingpatterns.com/contents.html
- [오토마타에 대해 알아봅시다.](https://m.blog.naver.com/PostView.nhn?blogId=staryoorang&logNo=80211270197&proxyReferer=https%3A%2F%2Fwww.google.com%2F)
- [오토마타](https://namu.wiki/w/%EC%98%A4%ED%86%A0%EB%A7%88%ED%83%80)
- 