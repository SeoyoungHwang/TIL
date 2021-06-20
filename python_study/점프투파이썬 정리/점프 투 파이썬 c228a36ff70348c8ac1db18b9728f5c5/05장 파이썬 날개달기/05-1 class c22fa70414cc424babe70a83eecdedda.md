# 05-1 class

## class는 왜 필요한가?

---

동일 기능을 수행하는 함수를 여러 번 사용하고자 하는경우

함수를 계속 생성하면서 서로 다른 변수에 저장하면 지장이 없지만 계속 함수와 전역 변수를 생성해야 하는 불편함이 있다.

클래스를 사용하여 객체를 생성하면 그 불편함을 줄일 수 있기 때문에 클래스를 사용하는 것이다.

클래스를 통해 만든 객체들이 각각의 역할을 수행하고 서로 독립적인 값을 가진다.

## class와 객체

---

![05-1%20class%20c22fa70414cc424babe70a83eecdedda/Untitled.png](05-1%20class%20c22fa70414cc424babe70a83eecdedda/Untitled.png)

과자 틀: 클래스

틀에 의해 만들어진 과자: 객체(object)

class: 똑같은 것을 계속해서 만들어 낼 수 있는 설계 도면

객체: 클래스로 만든 피조물

객체는 각각 고유한 성격을 가짐(서로 영향을 주지 않음)

```jsx
class Cookie:
    pass

a=Cookie()
b=Cookie()
```

a,b는 객체(Cookie()의 instance)

[객체와 인스턴스의 차이](https://www.notion.so/eng-ver-6076f9a5792c44a4b7171cd4fef69a57)

## 사칙연산 class 만들기

---

### class를 어떻게 만들지 먼저 구상하기

클래스로 만든 객체를 중심으로 어떤 식으로 동작하게 할 것인지 미리 구상 후 완성해 나가기

### class 구조 만들기

```jsx
>>> class FourCal:
...     pass
...
```

pass: 아무것도 수행하지 않는 문법, 임시로 코드를 작성할 때 사용

```jsx
>>> a=FourCal()
>>> type(a)
<class '__main__.FourCal'>
```

### 객체에 숫자 지정할 수 있게 만들기

a 객체에 사칙연산을 할 때 사용할 2개 숫자를 지정하는 것부터 시작

→ 그 기능을 하는 함수 만들기

```jsx
def setdata(self, first, second):
        self.first = first
        self.second = second
```

클래스 안에 구현된 함수: 메서드(Method)

**① setdata 메서드의 매개변수**

매개변수 self, first, second

`first`, `second`: 연산에 사용될 숫자들

`self`: `setdata`method를 호출한 객체 a가 자동으로 전달(self는 객체 a) 관례적으로 self 사용(객체를 호출할 때 호출한 객체 자신이 전달되기 때문)

![05-1%20class%20c22fa70414cc424babe70a83eecdedda/Untitled%201.png](05-1%20class%20c22fa70414cc424babe70a83eecdedda/Untitled%201.png)

**[메서드의 또 다른 호출 방법]**

클래스를 통해 호출하는 것도 가능(이 경우 `setdata` 호출시 객체를 첫번째 매개변수 `self`에 꼭 전달 해주어야 함)

객체.메서드 형태로 호출 시에는 self를 반드시 생략해서 호출)

```jsx
>>> a=FourCal()
>>> FourCal.setdata(4,2)
**Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
TypeError: setdata() missing 1 required positional argument: 'second'**
>>> FourCal.setdata(a,4,2)
>>> a.first
4
>>> a.second
2
>>> a.setdata(1,3)
>>> a.first
1
>>> a.second
3
>>> a.setdata(a,2,3)
**Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
TypeError: setdata() takes 3 positional arguments but 4 were given**
```

**② setdata 메서드의 수행문**

```jsx
def setdata(self, first, second):
        self.first = first
        self.second = second
```

`a.setdata(1,3)` 호출시 `setdata` method의 argument `first`, `second`에는 각각 값이 전달됨

`>>> a.first = 6` 수행시 a 객체에 객체변수 first 생성, 값 6이 저장됨

*객체변수: 객체에 생성되는 객체만의 변수*

클래스에 다른 객체가 생성된 경우 서로의 객체변수값에 영향을 미치지 않는다.

**클래스로 만든 객체의 객체변수에 상관없이 독립적인 값을 유지**

각각 객체변수 주소값이 다름 

### 더하기, 곱하기, 빼기, 나누기 기능 만들기

메서드 호출시 값이 출력되는 기능

```jsx
def add(self):
        result = self.first+self.second
        return result
```

매개변수: `self`

반환값: `result`

## 생성자(Constructor)

---

```jsx
a=FourCal()
a.add()
**Traceback (most recent call last):
AttributeError: 'FourCal' object has no attribute 'first'**
```

`setdata` 메서드를 수행하지 않고 다른 메서드 수행시 오류 발생

`setdata`를 수행해야 객체 변수가 생성되기 때문

객체에 초깃값을 설정할 필요가 있을 때 별도로 메서드를 생성하는 것보다는 생성자를 구현하는 것이 안전

생성자: 객체가 생성될 때 자동으로 호출되는 메서드

메서드를  `__init__`  으로 네이밍할 경우 생성자가 됨.

임의로 생성한 setdata와 코드가 똑같지만 메서드 이름이 `__init__`  이기 때문에 생성자로 인식됨

**생성자는 객체가 생성되는 시점에 자동으로 호출됨**

Constructor를 사용하는 경우

a=FourCal()에서 오류 발생.

객체 생성시 초깃값이 설정되지 않았기 때문에 오류 발생

```jsx
[pylint] E1120:No value for argument 'first' in constructor call
[pylint] E1120:No value for argument 'second' in constructor call
```

setdata()메소드를 사용한 경우 a=FourCal() 선언시 오류 발생하지 않음!

`__init__`   메서드도 마찬가지로 첫번째 매개변수 self에 생성되는 객체가 자동으로 전달됨

## class의 상속

---

클래스 생성시 다른 클래스의 기능을 물려받을 수 있게 만드는 것

예시: 상속 개념을 사용하여 FourCal()클래스에 제곱 기능 추가하기

상속한 클래스는 부모 클래스의 모든 기능을 사용할 수 있음

```jsx
class MoreFourCal(FourCal): 
    pass
**//상속 클래스 생성 방법**
    
a=MoreFourCal(3,5)

print(a.add())
print(a.mul())
print(a.sub())
print(a.div())
```

**상속을 하는 이유**

기존 클래스를 변경하지 않고 기능을 추가하거나 기존 기능을 변경하고자 할 때 사용함

기존 클래스가 라이브러리 형태로 제공되거나 수정이 허용되지 않는 경우 상속을 사용

```jsx
class MoreFourCal(FourCal): 
    def pow(self):
        result = self.first**self.second
        return result
```

기존 클래스를 그대로 놔두고 클래스의 기능을 확장시킬 때 주로 사용

## method overriding

---

```jsx
Traceback (most recent call last):
 line 37, in <module>
    print(a.div())
 line 20, in div
    result = self.first/self.second
ZeroDivisionError: division by zero
```

4/0은 계산이 안되기 때문에 오류가 발생함

오류가 아닌 다른 값을 반환하도록 만들고 싶을 경우 메서드 오버라이딩을 통해서 해결

메서드 오버라이딩: 부모 클래스에 있는 메서드를 **동일한 이름으로 재생성**

메서드 오버라이딩을 할 경우 부모클래스의 메서드 대신 오버라이딩한 메서드가 호출됨.

(쉽게 말해 메서드 덮어쓰기?)

```jsx
class SafeFourCal(FourCal):
    def div(self):
        if self.second==0: #나누는 값이 0일 경우 리턴값이 0
            return 0
        else:
            return self.first/self.second
```

```jsx
print(a.add())
print(a.mul())
print(a.sub())
**print(a.div())**
print(a.pow())
4
0
4
**0**
1

//pow()메소드를 SafeFourCal()에 삽입했다.
```

ZeroDivisionError가 발생하지 않고 0을 리턴함.

## class 변수

---

```jsx
>>> a=Family()
>>> b=Family()
>>> a.lastname
'kim'
>>> b.lastname
'kim'
>>> Family.lastname='park'
>>> a.lastname
'park'
>>> b.lastname
'park'
```

Family 클래스에 있는 변수가 변경될 경우 객체변수에 있는 동일한 이름의 변수도 변경됨.

```jsx
>>> id(Family.lastname)
2058771896496
>>> id(a.lastname)
2058771896496
>>> id(b.lastname)
2058771896496
```

변수를 공유함

class 내에서 선언된 변수는 객체변수와 같은 메모리를 가리키고 있음

클래스 변수는 클래스로 만든 모든 객체에 공유됨.