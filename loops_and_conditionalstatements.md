# Conditional Statements

## if ... elif ... else

##### syntax: `if`/`elif` + _condition_  , where _condition_ is a Boolean

```python
if True:
    print('True')        # -> True

if False:
    print('False')
      
if 1:
    print('1 = True')    # -> 1 = True

if 2:
    print('2 = True')    # -> 2 = True
    
if 0:
    print('0 = True')

if 'a':
    print('a = True')    # -> a = True
```

- _condition_ can include `and`, `or`, `in`, `not`, etc.
- Boolean:
    - `0, 0.0, (), [], {}, '', None` will convert to `False`
    - All else will convert to `True`

##### 'pass' means do nothing

```python
>>> if 1 > 2:
>>>     pass
>>> else:
>>>     print('Pass means do nothing')
Pass means do nothing
```

.

##### when Indexing Variable is not used within the loop, use `_`

```python
for _ in range(10):       # (X) for i in range(10):
    print("Hi")
```

.

## short-hand version

=> _valueWhenTrue_ `if` _condition_ `else` _valueWhenFalse_

타 언어의 삼항 연산자와 동일하다

```python
>>> num = 5
>>> print('num > 5') if num > 5 else print('num <= 5')
num <= 5
```

```python
>>> userinput = int(input("Enter integer: "))
>>> positivevalue = userinput if userinput > 0 else 0
>>> print(positivevalue)
# (5 -> 5  /  -3 -> 0)
```

.

.

# while loop

조건식이 True인 경우 반복적으로 코드를 실행한다. 

따라서 반드시 종료조건을 설정해주어야 한다. (Or else, will result in an infinite loop)

- use `break`, `continue`

##### Vending Machine - Coffee

```python
price = 300
left = 10
money = 0

while left >= 1:
    money += int(input("Insert cash: "))
    if money < 300:
        print("Not enough cash")
        continue
    else:
        while True:
            cnt = int(input(f"커피 몇 잔? (balance: {money}) => "))
            if cnt > left:
                print(f'Not enough coffee. Only {left} available')
                continue
            if money >= 300 * cnt:
                left -= cnt
                print(f'Result: 커피 {cnt}잔  ({left}잔 remaining)')
                if money > 300 * cnt:
                    money -= 300 * cnt
                    print(f'Change: {money}')
                    money = 0
                elif money == 300 * cnt:
                    money = 0
                break
            else:
                print('Not enough cash\n')
                choice = input('Choose: 1) Insert more cash  or  2) Less coffee => ')
                if choice == '1':
                    break
                elif choice == '2':
                    continue
    print()

print('Out of stock')
```





.

.

# for loop

##### for loops and scope

- `for` loops (along with `if` statements) do NOT create a separate scope.

- The iterating variable used in the for loops may be used elsewhere

  ```python
  for i in [1, 2, 3]:
      print(i)          # at the end of this loop, i == 3
  print(i)
  
  ## Result:
  # 1
  # 2
  # 3
  # 3
  ```

  ```python
  for i in [1, 2, 3]:
      print("hi")       # at the end of this loop, i == 3
  
  def func1():
      print(i)          # this function can also access "i"
  
  func1()
  
  ## Result:
  # hi
  # hi
  # hi
  # 3
  ```


##### for loops and dictionaries

for `dict1 = {'A': 65, 'B': 66, 'C': 67}`   :

```python
>>> for key in dict1:
>>>     print('key: ', key)
>>>     print('value: ', dict1[key])
key:  A
value:  65
key:  B
value:  66
key:  C
value:  67
```

```python
>>> print(dict1.items())
>>> for key, val in dict1.items():
>>>     print('key: ', key)
>>>     print('value: ', val)
dict_items([('A', 65), ('B', 66), ('C', 67)])
key:  A
value:  65
key:  B
value:  66
key:  C
value:  67
```

##### for loops and 다차원 리스트

```python
>>> a = [(1, (2.1, 2.2), 3), 
>>>      (10, 20, 30), 
>>>      (100, 200, 300)]

>>> for num in a:
>>>     print(num)    # 1차원 아이템 출력
(1, (2.1, 2.2), 3)
(10, 20, 30)
(100, 200, 300)

>>> for first, second, third in a:
>>>     print('first:', first)
>>>     print('second:', second) # argument 'third' is not used
first: 1
second: (2.1, 2.2) 
first: 10
second: 20 
first: 100
second: 200
# 3 arguments (first, second, third) : the length of each and every item in the list must also be '3'
```

##### 별 찍기: Right Triangle

```python
h = int(input("Enter triangle height: "))
for x in range(1, h+1):
    print(f"{'*'*x}")

# result (when h = 3):
# *
# **
# ***
```

##### 별 찍기: Christmas Tree

```python
h = int(input("Enter triangle height: "))
for x in range(1, h+1):
    print(f"{' '*(h-x)}", end='')
    print(f"{'*'*(2*x-1)}")

# result (when h = 3):
#   *
#  ***
# *****
```

##### 별 찍기: Upside-down Christmas Tree

```python
h = int(input("Enter triangle height: "))
for x in range(h, 0, -1):
    print(f"{' '*(h-x)}", end='')
    print(f"{'*'*(2*x-1)}")
```

##### Calendar 2019

```python
cnt = 2   # Jan 1, 2019 is a Tuesday
month = ['January', 'February', 'March', 'April', 'May', 'June', 
        'July', 'August', 'September', 'October', 'November', 'December']

print(f'{"= 2019 =":^21}\n')

for x in range(12):
    print(f'{month[x]+" 2019":^21}')
    print(' S  M  T  W  T  F  S')
    
    if x+1 == 2:
        enddate = 28
    elif x+1 in [1, 3, 5, 7, 8, 10, 12]:
        enddate = 31
    elif x+1 in [4, 6, 9, 11]:
        enddate = 30
    
    print(' '*cnt*3, end='')
    
    for y in range(1, enddate+1):
        print(f'{y:>2}', end=' ')
        cnt += 1
        if cnt == 7:
            print()
            cnt = 0

    if cnt != 0:
        print()
    
    print()
```





# Try ... Except

### Handling anticipated errors

- `try`: execute when no errors are raised
- `except`: execute when an error _is_ raised
- `except ~~Error`: execute only when the specified type of error is raised
  - e.g) NameError, IndexError, SyntaxError, ModuleNotFoundError, KeyError, ImportError, TypeError, ValueError, ZeroDivisionError, ...
- `else`: execute when no errors are raised
  - (placed after `try ... except`)
- `finally`: always execute, error or no error

##### Ex) Without using `try ... except`

```python
s = "word"

for i in range(6):
    print(f"#{i}: {s[i]}")

##### result:
#0: w
#1: o
#2: r
#3: d
---------------------------------------------------------------------------
IndexError                                Traceback (most recent call last)
<ipython-input-27-f3211b1689cd> in <module>()
      2 
      3 for i in range(6):
----> 4     print(f"#{i}: {s[i]}")

IndexError: string index out of range
```

##### Ex) With `try ... except`

```python
s = "word"

for i in range(6):
    try:
        print(f"#{i}: {s[i]}")
    except:
        print(f"#{i}: No more letters to print")

##### result:
#0: w
#1: o
#2: r
#3: d
#4: No more letters to print
#5: No more letters to print
```

##### Ex) `try ... except ... else ... finally`

```python
s = "word"

for i in range(6):
    try:
        print(f"#{i}: {s[i]}")
    except IndexError:
        print(f"#{i}: IndexError - No more letters to print")
    except:
        print("Other type of error")
    else:
        print("Else - No errors")
    finally:
        print("Finally - Always Execute\n")
        
##### result:
#0: w
Else - No errors
Finally - Always Execute

#1: o
Else - No errors
Finally - Always Execute

#2: r
Else - No errors
Finally - Always Execute

#3: d
Else - No errors
Finally - Always Execute

#4: IndexError - No more letters to print
Finally - Always Execute

#5: IndexError - No more letters to print
Finally - Always Execute
```

























