파이썬의 핵심 객체와 자료형 (Data Types)
파이썬은 모든 것이 객체(Object)로 이루어져 있는 객체 지향 언어입니다. 우리가 사용하는 숫자, 문자열, 리스트 등 모든 데이터는 메모리에 존재하는 특정 타입의 객체입니다.

1. 파이썬의 핵심 객체를 확인하는 방법
.__class__ 속성: 객체가 어떤 클래스(타입)의 인스턴스인지를 보여줍니다.
type() 함수: 특정 객체의 타입을 반환합니다. .__class__와 동일한 결과를 보여줍니다.
<!-- end list -->

Python

x = 100
print(x.__class__)          # <class 'int'> : x는 int 클래스의 인스턴스입니다.
print(type(x))              # <class 'int'> : x의 타입은 int입니다.

# 클래스(타입) 자체도 객체입니다.
# int 클래스 객체는 type 클래스의 인스턴스입니다.
print(x.__class__.__class__) # <class 'type'>
print(type(type(x)))         # <class 'type'>
isinstance(obj, classinfo) 함수: obj가 classinfo의 인스턴스인지 (또는 classinfo를 상속받은 클래스의 인스턴스인지) True 또는 False로 반환합니다.
<!-- end list -->

Python

x = 100
print(isinstance(x, int))   # True : x는 int의 인스턴스입니다.
print(isinstance(x, float)) # False: x는 float의 인스턴스가 아닙니다.
2. Built-in 데이터 타입 (내장 자료형)
파이썬이 기본적으로 제공하는 주요 데이터 타입들입니다.

2.1. 숫자형 (Numbers): int, float, bool
int (정수형): 소수점 없는 정수 (100, -5).
float (실수형): 소수점이 있는 숫자 (100.0, 3.14).
bool (논리형): 참(True) 또는 거짓(False)을 나타냅니다.
주의: True와 False는 반드시 첫 글자를 대문자로 써야 합니다.
bool은 int의 서브클래스입니다. 따라서 True는 1로, False는 0으로 해석됩니다.
<!-- end list -->

Python

x = 100
print(isinstance(x, int))   # True

y = 100.0
print(isinstance(y, float)) # True

z = True
print(isinstance(z, int))   # True (bool은 int의 서브클래스이므로)
print(isinstance(z, float)) # False
print(isinstance(z, bool))  # True
print(True == 1)            # True
print(False == 0)           # True
2.2. 문자열 (String): str
따옴표('', "", """ """, ''' ''')로 감싸서 표현합니다.
순서가 있는(Sequence) 자료형으로, 문자 하나하나가 순서대로 저장됩니다. 인덱싱을 통해 각 문자에 접근할 수 있습니다.
**수정 불가능(Immutable)**한 자료형입니다. 한 번 생성된 문자열은 내용을 변경할 수 없습니다.
<!-- end list -->

Python

x = "안녕하세요"
print(x[0])         # '안'
print(x[len(x) - 1]) # '요' (마지막 문자)
# x[0] = '하' # TypeError: 'str' object does not support item assignment
2.3. 리스트 (List): list
대괄호 [] 안에 객체들을 순서대로 모아 놓은 객체입니다.
각 요소는 메모리 주소를 통해 참조되며, 인덱싱으로 접근 가능합니다.
다양한 타입의 객체를 함께 저장할 수 있습니다.
**수정 가능(Mutable)**한 자료형입니다. 요소 추가, 삭제, 변경이 자유롭습니다.
<!-- end list -->

Python

x = ["안녕하세요", 1, 2, [1, 2]]
print(isinstance(x, list)) # True
print(type(x))             # <class 'list'>
print(len(x))              # 4 (리스트 안에 들어있는 객체의 수)
x.append("새로운 요소")
print(x)                   # ['안녕하세요', 1, 2, [1, 2], '새로운 요소']
x[0] = "안녕"
print(x)                   # ['안녕', 1, 2, [1, 2], '새로운 요소']
2.4. 튜플 (Tuple): tuple
괄호 () 안에 객체들을 순서대로 모아 놓은 객체입니다.
리스트와 유사하게 다양한 타입의 객체를 저장할 수 있고 인덱싱으로 접근 가능합니다.
**수정 불가능(Immutable)**한 자료형입니다. 한 번 생성된 튜플은 요소를 변경할 수 없습니다.
<!-- end list -->

Python

x = (1, 2, 3, 4, [5, 6]) # 튜플 자체는 수정 불가능하지만, 튜플 안의 리스트는 수정 가능
print(x, isinstance(x, tuple)) # (1, 2, 3, 4, [5, 6]) True

# 한 개의 요소로 이루어진 튜플을 만들 때는 쉼표(,)를 반드시 붙여야 합니다.
y = (1)
print(isinstance(y, tuple)) # False: (1)은 단순히 괄호로 묶인 정수 1로 해석됨
z = (1, ) # 쉼표가 붙으면 튜플로 인식됩니다.
print(isinstance(z, tuple)) # True
2.5. 딕셔너리 (Dictionary): dict
중괄호 {} 안에 key: value 쌍 형태로 객체들을 저장합니다.
순서가 없습니다. (Python 3.7+부터 삽입 순서가 보장되지만, 여전히 인덱싱으로 접근하는 순서 자료형은 아닙니다.)
key의 조건:
고유해야 합니다. 중복된 key가 있으면 나중에 추가된 key: value 쌍이 이전 것을 덮어씁니다.
수정 불가능(Immutable)하고 해시 가능(Hashable)한 자료형만 key로 사용할 수 있습니다. (numbers, str, tuple, frozenset 등) bool도 가능합니다.
value의 조건: 어떤 자료형이든 들어갈 수 있으며, 중복도 가능합니다.
**수정 가능(Mutable)**한 자료형입니다. 새로운 key: value 추가, 기존 value 변경, key: value 삭제가 자유롭습니다.
<!-- end list -->

Python

x = {
    "name": "Gyu",
    "age": 24,
    "hobby": ["롤", "맨몸운동", "배드민턴"],
    "age": 32 # 'age' 키가 중복되므로, 24는 32로 덮어쓰여집니다.
}
print(isinstance(x, dict)) # True
print(type(x))             # <class 'dict'>
print(x["name"])           # Gyu
print(x["age"])            # 32 (덮어씌워진 값)
print(x["hobby"])          # ['롤', '맨몸운동', '배드민턴']
print(len(x))              # 3 (키는 name, age, hobby 3개)

x["address"] = "동대문구"  # 없는 키에 접근 시 새로운 key:value 쌍 생성
print(x)                   # {'name': 'Gyu', 'age': 32, 'hobby': ['롤', '맨몸운동', '배드민턴'], 'address': '동대문구'}
x["address"] = "청량리"    # 있는 키에 접근 시 해당 키의 value 수정
print(x)                   # {'name': 'Gyu', 'age': 32, 'hobby': ['롤', '맨몸운동', '배드민턴'], 'address': '청량리'}
2.6. 셋 (Set): set
중괄호 {} 안에 객체들을 모아 놓은 객체입니다.
순서가 없습니다. (딕셔너리와 유사)
중복을 허용하지 않습니다. 중복되는 요소를 추가하면 자동으로 제거됩니다.
set 안에 들어가는 요소는 수정 불가능(Immutable)하고 해시 가능(Hashable)한 자료형이어야 합니다. (딕셔너리의 key와 동일한 조건)
따라서 list, dict, set 자체는 set의 요소가 될 수 없습니다. frozenset은 가능합니다.
**수정 가능(Mutable)**한 자료형입니다. 요소 추가, 삭제가 가능합니다.
<!-- end list -->

Python

# x = {[1, 2, 3], [5, 6, 7]} # TypeError: unhashable type: 'list'

x = {1, 2, 3, 4, 5, 5, 5, 6, 2, 7}
print(x, isinstance(x, set)) # {1, 2, 3, 4, 5, 6, 7} True (중복이 제거되어 출력)
print(type(x))               # <class 'set'>

x.add(8)                     # 요소 추가
print(x)                     # {1, 2, 3, 4, 5, 6, 7, 8}
x.remove(1)                  # 요소 삭제
print(x)                     # {2, 3, 4, 5, 6, 7, 8}
2.7. NoneType: None
**None**은 값이 없거나, 아무것도 참조하지 않음을 나타내는 특별한 객체입니다.
NoneType은 None 객체의 타입 이름입니다. isinstance(x, NoneType)처럼 직접 NoneType을 사용하는 대신, is x is None 또는 type(x) is type(None)과 같이 확인하는 것이 일반적입니다.
어떤 함수가 명시적으로 값을 반환하지 않을 때 기본적으로 None을 반환합니다.
<!-- end list -->

Python

x = None
print(x, type(x))            # None <class 'NoneType'>
print(x is None)             # True
# print(isinstance(x, NoneType)) # NameError: name 'NoneType' is not defined (NoneType은 직접 접근하는 클래스 이름이 아닙니다.)
3. Hash Table (해시 테이블)과 key의 조건
dict와 set은 내부적으로 해시 테이블(Hash Table) 이라는 자료구조를 사용하여 데이터를 저장하고 검색합니다.
데이터를 저장할 때, key (또는 set의 요소)의 **해시값(hash value)**을 계산하여 그 해시값에 해당하는 메모리 위치에 value를 저장합니다.
데이터를 검색할 때도 동일한 key의 해시값을 계산하여 저장된 위치를 빠르게 찾습니다.
key가 수정 불가능한 타입이어야 하는 이유:
만약 key가 수정 가능한 객체라면, key의 내용이 바뀔 때 해시값도 바뀔 수 있습니다.
해시값이 바뀌면 dict나 set이 원래 저장했던 해시값과 현재 key의 해시값이 달라져, 해당 key로 value를 찾을 수 없게 되거나 내부 구조가 손상될 수 있습니다.
따라서 key는 수정 불가능(Immutable)하면서 해시 가능(Hashable)한 객체여야 합니다.
4. Mutable (수정 가능) vs Immutable (수정 불가능)
메모리에 저장된 객체의 값을 변경할 수 있는지에 대한 중요한 개념입니다.

수정 가능한(Mutable) 데이터:

객체의 내용(값)을 변경해도 메모리 주소는 동일하게 유지됩니다.
예: list, dict, set
수정 불가능한(Immutable) 데이터:

객체의 내용(값)을 변경하려고 하면 새로운 객체가 생성되고 새로운 메모리 주소를 가리키게 됩니다. 기존 객체는 변경되지 않습니다.
예: numbers (int, float, bool), str, tuple, frozenset
<!-- end list -->

Python

# Mutable 예시: list
list1 = [1, 2, 3]
list2 = list1
print(id(list1), id(list2)) # 동일한 메모리 주소
list2.append(4)
print(list1)                # [1, 2, 3, 4] (list1도 변경됨)
print(id(list1), id(list2)) # 여전히 동일한 메모리 주소

# Immutable 예시: int
int1 = 10
int2 = int1
print(id(int1), id(int2)) # 동일한 메모리 주소
int2 = 20                 # int2에 새로운 값을 할당 (새로운 객체 생성)
print(int1)               # 10 (int1은 변경되지 않음)
print(id(int1), id(int2)) # 서로 다른 메모리 주소
이러한 파이썬의 기본 자료형과 객체 지향 원리를 이해하는 것은 파이썬 프로그래밍의 기초를 튼튼히 하는 데 매우 중요합니다.
