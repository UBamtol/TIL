# 변수

## 변수란 무엇인가? 왜 필요한가?

변수(variable)는 하나의 값을 저장하기 위해 확보한 메모리 공간 자체 또는 그 메모리 공간을 식별하기 위해 붙인 이름을 말한다.

간단히 말하면 변수는 프로그래밍 언어에서 값을 저장하고 참조하는 메커니즘으로, 값의 위치를 가리키는 상징적인 이름이다.

💡**변수에 여러 개의 값을 저장하는 방법**</br>
변수는 하나의 값을 저장하기 위한 메커니즘이다. 여러 개의 값을 저장하려면 여러 개의 변수를 사용해야 한다. 단, 배열이나 객체 같은 구조를 사용하면 관련이 있는 여러 개의 값을 그룹화해서 하나의 값처럼 사용할 수 있다.

```jsx
 ex)
// 변수는 하나의 값을 저장하기 위한 수단이다.
var = useId = 1;
var = userName = ‘Yu’;

// 객체나 배열 같은 자료구조를 사용하면 여러 개의 값을 하나로 그룹화해서 하나의 값처럼 사용할 수 있다.
var user { id: 1, name: ‘Yu’ };

var users = [
  { id: 1, name: ‘Yu’ },
  { id: 2, name: ‘Kim’},
];
```

**변수 이름(변수명)** : 메모리 공간에 저장된 값을 식별할 수 있는 고유한 이름

**변수 값** : 변수에 저장된 값

**할당(대입, 저장)** : 변수에 값을 저장하는 것

**참조** : 변수에 저장된 값을 읽어들이는 것

## 식별자

변수 이름을 식별자라고도 한다. **식별자는 어떤 값을 구별해서 식별할 수 있는 고유한 이름을 말한다**.

값은 메모리 공간에 저장되어 있다. 따라서 식별자는 메모리 공간에 저장되어 있는 어떤 값을 구별해서 식별해낼 수 있어야 한다. 이를 위해 식별자는 어떤 값이 저장되어 있는 메모리 주소를 기억해야 한다.

**식별자는 값이 아니라 메모리 주소를 기억하고 있다.** 식별자로 값을 구별해서 식별한다는 것은 식별자가 기억하고 있는 메모리 주소를 통해 메모리 공간에 저장된 값에 접근할 수 있다는 의미이다.

즉, 메모리 상에 존재하는 어떤 값을 식별할 수 있는 이름은 모두 식별자라고 한다.

변수, 함수, 클래스 등의 이름과 같은 식별자는 네이밍 규칙을 준수해야하며, **선언**에 의해 자바스크립트 엔진에 식별자의 존재를 알린다.

## 변수 선언

변수 선언이란 변수를 생성하는 것을 말한다. 좀 더 자세히 말하면 값을 저장하기 위한 메모리 공간을 확보하고 변수 이름과 확보된 메모리 공간의 주소를 연결해서 값을 저장할 수 있게 준비하는 것이다. 변수 선언에 의해 확보된 메모리 공간은 확보가 해제되기 전까지는 누구도 확보된 메모리 공간을 사용할 수 없도록 보호되므로 안전하게 사용할 수 있다.

변수를 사용하려면 반드시 선언이 필요하다. 변수를 선언할 때는 var, let, const 키워드를 사용한다.

ES6에서 let, const 키워드가 도입되기 전까지는 var 키워드는 자바스크립트에서 변수를 선언할 수 있는 유일한 키워드였다.

💡**ES5 vs ES6**</br>
var에는 여러 단점이 있다. var 키워드의 여러 단점 중에 가장 대표적인 것이 블록 레벨 스코프를 지원하지 않고 함수 레벨 스코프를 지원한다는 것이다. 이로 인해 의도치 않게 전역 변수가 선언되어 심각한 부작용을 발생시키기도 한다.

```jsx
var = score; // 변수 선언(변수 선언문)
```

변수를 선언한 이후, 아직 변수에 값을 할당하지 않았다. 따라서 변수의 메모리 공간이 비어있다고 생각할 수 있지만 확보된 메모리 공간에는 자바스크립트 엔진에 의해 undefined라는 값이 암묵적으로 할당되어 초기화된다. 이것은 자바스크립트의 독특한 특징이다.

자바스크립트 엔진은 변수 선언을 다음과 같이 2단계에 거쳐 수행한다.

1. **선언 단계:** 변수 이름을 등록해서 자바스크립트 엔진에 변수의 존재를 알린다.
2. **초기화 단계:** 값을 저장하기 위한 메모리 공간을 확보하고 암묵적으로 undefined를 할당해 초기화 한다.

만약 초기화 단계를 거치지 않으면 확보된 메모리 공간에는 이전에 다른 애플리케이션이 사용했던 값이 남아있을 수 있다. 이러한 값을 쓰레기 값이라고 한다. 따라서 메모리 공간을 확보한 다음, 값을 할당하지 않은 상태에서 곧바로 변수 값을 참조하면 쓰레기 값이 나올 수 있다.

## 변수 선언의 실행 시점과 변수 호이스팅

```jsx
console.log(score); // undefined
var score; // 변수 선언문
```

변수 선언문보다 변수를 참조하는 코드가 앞에 있다. 자바스크립트 코드는 인터프리터에 의해 한 줄씩 순차적으로 실행되므로 console.log(score);가 가장 먼저 실행되고 순차적으로 다음 줄에 있는 코드를 실행한다. 따라서 console.log(score);가 실행되는 시점에는 아직 score 변수의 선언이 실행되지 않았으므로 참조 에러가 발생한 것처럼 보인다. 하지만 참조 에러가 발생하지 않고 undefined가 출력된다.

그 이유는 **변수선언이 소스코드가 한 줄씩 순차적으로 실행되는 시점, 즉 런타임이 아니라 그 이전 단계에서 먼저 실행되기 때문이다.**

자바스크립트 엔진은 소스코드를 한 줄씩 순차적으로 실행하기에 앞서 먼저 소스코드의 평가 과정을 거치면서 소스코드를 실행하기 위한 준비를 한다. 이때 소스코드 실행을 위한 준비 단계인 소스코드의 평가 과정에서 자바스크립트 엔진은 변수 선언을 포함한 모든 선언문(변수 선언문, 함수 선언문 등)을 소스코드에서 찾아내 먼저 실행한다. 그리고 소스코드의 평가 과정이 끝나면변수 선언을 포함한 모든 선언문을 제외하고 한 줄씩 순차적으로 실행한다.

즉, 자바스크립트 엔진은 변수 선언이 소스코드의 어디에 있든 상관없이 다른 코드보다 먼저 실행한다. 따라서 변수 선언이 소스코드의 어디에 위치하는지와 상관없이 어디서든지 변수를 참조할 수 있다. 이처럼 **변수 선언문이 코드의 선두로 끌어 올려진 것처럼 동작하는 자바스크립트 고유의 특징을 호이스팅이라고 한다.** 변수 선언뿐 아니라 var, letl const, function, function\*, class 키워드를 사용해서 선언하는 모든 식별자(변수, 함수, 클래스 등)는 호이스팅된다. 모든 선언문은 런타임 이전 단계에서 먼저 실행되기 때문이다.

## 값의 할당

변수에 값을 할당(대입, 저장)할 때는 할당 연산자=를 사용한다. 할당 연산자는 우변의 값을 좌변의 변수에 할당한다.

```jsx
var score; // 변수 선언
score = 80; // 값의 할당
// 변수 선언과 값의 할당을 하나의 문으로 단축 표현할 수도 있다.
var score = 80; // 변수 선언과 값의 할당
```

이때 주의할 점은 변수 선언과 값의 할당의 실행 시점이 다르다는 것이다. **변수 선언은 소스코드가 순차적으로 실행되는 시점인 런타임 이전에 먼저 실행되지만 값의 할당은 소스코드가 순차적으로 실행되는 시점인 런타임에 실행된다.**

```jsx
console.log(score); // undefined
var score; // 1.변수 선언
score = 80; // 2.값의 할당
console.log(score); // 80
```

변수 선언(1)은 런타임 이전에 먼저 실행되고 값의 할당(2)은 런타임에 실행된다. 따라서 score 변수에 값을 할당하는 시점(2)에는 이미 변수 선언이 완료된 상태이며, 이미 undefined로 초기화되어 있다. 따라서 score 변수에 값을 할당하면 score 변수의 값은 undefined에서 새로 할당한 숫자 값인 80으로 변경(재할당)된다.

변수 선언과 값의 할당을 하나의 문으로 단축 표현해도 자바스크립트 엔진은 변수의 선언과 값의 할당을 2개의 문으로 나누어 각각 실행한다.

## 값의 재할당

```jsx
var score = 80; // 변수 선언과 값의 할당
score = 90; // 값의 재할당
```

var, let 키워드로 선언한 변수는 값을 재할당 할 수 있다. **재할당은 현재 변수에 저장된 값을 버리고 새로운 값을 저장하는 것이다. 만약 값을 재할당할 수 없어서 변수에 저장된 값을 변경할 수 없다면 변수가 아니라 상수(const)라 한다.** 상수는 한번 정해지면 변하지 않는 값이다.

현재 score 변수의 값은 90이다. score 변수의 이전 값인 undefined와 80은 어떤 변수도 값으로 갖고 있지 않다. 다시 말해, 어떤 식별자와도 연결되어 있지 않다. 이것은 undefined 와 80이 더이상 필요하지 않다는 것을 의미한다. 이러한 불필요한 값들은 **가비지 콜렉터**에 의해 메모리에서 자동 해제된다.

💡 **가비지 콜렉터**</br>
가비지 콜렉터는 애플리케이션이 할당한 메모리 공간을 주기적으로 검사하여 더 이상 사용되지 않는 메모리를 해제하는 기능을 말한다. 더 이상 사용되지 않는 메모리란 간단히 말하자면 어떤 식별자도 참조하지 않는 메모리 공간을 의미한다. 자바스크립트는 가비지 콜렉터를 내장하고 있는 매니지드 언어로서 가비지 콜렉터를 통해 메모리 누수를 방지한다.

💡 **언매니지드 언어와 매니지드 언어**
**언매니지드 언어**는 C언어와 같이 개발자가 명시적으로 메모리를 할당하고 해제하기 위해 malloc()과 free() 같은 저수준 메모리 제어 기능을 제공한다. 메모리 제어를 개발자가 주도할 수 있으므로 개발자의 역량에 따라 최적의 성능을 확보할 수 있지만 그 반대의 경우 치명적 오류를 생산할 가능성도 있다.
**매니지드 언어**는 자바스크립트와 같이 메모리 할당 및 해제를 위한 메모리 관리 기능을 언어 차원에서 담당하고 개발자의 직접적인 메모리 제어를 허용하지 않는다. 더 이상 사용하지 않는 메모리의 해제는 가비지 콜렉터가 수행한다. 개발자의 역량에 의존하는 부분이 상대적으로 작아져 어느 정도 일정한 생산성을 확보할 수 있지만 성능 면에서 어느 정도의 손실을 감수하여야 한다.

## 식별자 네이밍 규칙

- 식별자는 특수문자를 제외한 문자, 숫자, 언더스코어(\_), 달러 기호($)를 포함할 수 있다.
- 단, 식별자는 특수문자를 제외한 문자, 언더스코어(\_), 달러 기호($)로 시작해야하며, 숫자는 허용하지 않는다.
- 예약어는 식별자로 사용할 수 없다.

  ![image](https://user-images.githubusercontent.com/98325285/170542726-39fa3208-04ac-4bd8-b2a9-11535717fb2b.png)

**네이밍 컨벤션**은 하나 이상의 영어 단어로 구성된 식별자를 만들 때 가독성 좋게 단어를 한눈에 구분하기 위해 규정한 명명 규칙이다.

```jsx
// 카멜 케이스(camelCase)
var firstName;

// 스네이크 케이스(snake_case)
var first_name;

// 파스칼 케이스(PascalCase)
var FirstName;

// 헝가리언 케이스(typeHungarianCase)
var strFirtstName; // type + identifier
var $elem = document.getElementById('myId'); // DOM 노드
var observable$ = fromEvent(document, 'click'); // RxJS 옵저버블
```

자바스크립트에서는 일반적으로 변수나 함수의 이름에는 **카멜케이스,** 생성자 함수, 클래스의 이름에는 **파스칼 케이스**를 사용한다.
