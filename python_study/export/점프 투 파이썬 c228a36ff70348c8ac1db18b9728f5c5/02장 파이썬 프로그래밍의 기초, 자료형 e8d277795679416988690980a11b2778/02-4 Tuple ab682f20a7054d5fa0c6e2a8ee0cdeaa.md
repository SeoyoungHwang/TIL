# 02-4 Tuple

> List: mutable
Tuple: immutable

## 1. 튜플은 어떻게 만들까?

---

튜플과 리스트의 차이

- 리스트 [] / 튜플 ()
- 리스트: 값 생성 수정 가능 / 튜플: 불가능
    - 변수 변화여부에 따라 튜플/리스트 선언!

```python
>>> tp=()
>>> tp=(1,)
>>> tp
(1,)
//한개의 요소를 가질 때에는 콤마를 반드시 붙여야함
>>> tp=(2)
>>> tp
2 //아니면 변수선언이 됨..

>>> tp=1,2 //괄호 생략해도 무방
>>> tp
(1, 2)
>>> tp=(1,2,(3,4,5))
>>> tp
(1, 2, (3, 4, 5))

```

## 2. 튜플의 요소값을 지우거나 변경하려고 하면 어떻게 될까?

---

```python
>>> del tp[0]
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
TypeError: 'tuple' object doesn't support item deletion

>>> tp[0]='c'
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
TypeError: 'tuple' object does not support item assignment
```

지우기 요소값 변경 안됨

## 3. 튜플 다루기

1. 인덱싱

    리스트와 마찬가지로 가능

2. 슬라이싱

    ```python
    >>> tp=(1, 2, (3, 4, 5))
    >>> tp[1:]
    (2, (3, 4, 5))
    >>> tp[2][:1]
    (3,)
    ```

3. 튜플 더하기

    string, list랑 동일

4. 튜플 곱하기

    string, list랑 동일

5. 튜플 길이 구하기

    string, list랑 동일