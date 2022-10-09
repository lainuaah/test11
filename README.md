# Class và Instance Variables
Trong Python, properties được chia làm 2 loại:
- Class variables
- Instance variables

![class-instance variables](variables.png)

## Class variables
Tất cả các objects của class đều được phép truy cập và thay đổi giá trị của **class variable**. Khi thay đổi giá trị của **class variable** thì giá trị của property này sẽ thay đổi trong tất cả các object của class.

## Instance variables
**Instance variables** là của riêng với mỗi objects. Sự thay đổi ở instance variables của object nào thì chỉ ảnh hưởng đến object đó.

## Khai báo class variable và instance variable
**Class variables** được khai báo ngoài `initializer` và **instance variables** được khai báo trong scope của `initializer`

```python
class Player:
    teamName = 'Manchester City'  # class variables

    def __init__(self, name):
        self.name = name  # creating instance variables
```

## Ví dụ về sử dụng class variable `sai`
Chúng ta phải sử dụng **class variable** đúng cách vì như đã nói, chúng a được chia sẻ cho tất cả các objects thuộc class và có thể thay đổi giá trị của **class variable** bằng cách sử dụng bất kỳ objects nào.

```python
class Player:
    teamName = 'Manchester City'  # class variables
    formerTeams = [] # class variables
    def __init__(self, name):
        self.name = name  # creating instance variables

p1 = Player("David Silva")
p2 = Player("Yaya Toure")

p1.formerTeams.append('Celta Vigo') # wrong use of class variable
p2.formerTeams.append('Barcelona') # wrong use of class variable

print("Name:", p1.name)
print("Team Name:", p1.teamName)
print(p1.formerTeams)
print("Name:", p2.name)
print("Team Name:", p2.teamName)
print(p2.formerTeams)
```
**Output**
```
Name: David Silva
Team Name: Manchester City
['Celta Vigo', 'Barcelona']
Name: Yaya Toure
Team Name: Manchester City
['Celta Vigo', 'Barcelona']
```

Ở ví dụ trên, trong khi **instance variable** `name` là riêng biệt cho mỗi object thuộc `Player` class. Thì **class variable** `formerTeams`, có thể truy cập bởi tất cả các object thuộc class nên nó đã được cập nhật giá trị. 

Chúng ta đang lưu trữ tất cả các cầu thủ hiện đang chơi cho cùng một đội, nhưng mỗi cầu thủ trong đội phần lớn sẽ không cùng đội bóng cũ. Để tránh vấn đề này, triển khai chính xác cho ví dụ trên sẽ như sau:

```python
class Player:
    teamName = 'Manchester City'  # class variables
    
    def __init__(self, name):
        self.name = name  # instance variables
        self.formerTeams = [] # instance variables

p1 = Player("David Silva")
p2 = Player("Yaya Toure")

p1.formerTeams.append('Celta Vigo') # wrong use of class variable
p2.formerTeams.append('Barcelona') # wrong use of class variable

print("Name:", p1.name)
print("Team Name:", p1.teamName)
print(p1.formerTeams)
print("Name:", p2.name)
print("Team Name:", p2.teamName)
print(p2.formerTeams)
```
**Output**
```
Name: David Silva
Team Name: Manchester City
['Celta Vigo']
Name: Yaya Toure
Team Name: Manchester City
['Barcelona']
```
Bây giờ, `formerTeams` đã là của riêng của mỗi `Player` object, và sẽ được truy cập bởi object đó mà thôi.

## Một ví dụ khác về sử dụng class variables
```python
class Player:
    teamName = 'Manchester City'      # class variables
    teamMembers = []

    def __init__(self, name):
        self.name = name        # creating instance variables
        self.formerTeams = []
        self.teamMembers.append(self.name)


p1 = Player('David Silva')
p2 = Player('Yaya Toure')

print("Team Name:", p1.teamName)
print("Team Members:")
print(p1.teamMembers)
print("")
print("Name:", p2.name)
print("Team Members:")
print(p2.teamMembers)
```

**Output**
```
Team Name: Manchester City
Team Members:
['David Silva', 'Yaya Toure']

Name: Yaya Toure
Team Members:
['David Silva', 'Yaya Toure']
```
Ở ví dụ trên, chúng ta đã khai báo `teamMembers`, một list được chia sẻ với tất cả các object thuộc `Player` class. Mỗi object `Player` được tạo ra, `name` của object sẽ được thêm vào list `teamMembers`, chúng ta có thể thấy `p1` và `p2` đều có thể truy cập vào `teamMembers`.

# Methods trong một Class
Trong phần này, chúng ta sẽ xem về chuyện tương tác giữa ``properties`` và các ``objects``. Đây là lúc ``methods`` xuất hiện, có 3 loại `method` trong Python:
1. **instance methods**
2. **class methods**
3. **static methods**

> `Note`: Chúng ta sẽ gọi **method** cho **instance method** vì nó thường được sử dụng nhất.

## Instance Method

> **`Methods`** là một nhóm các statements (câu lệnh) thực hiện một số thao tác (operations) và có thể trả về (return) hoặc không trả về một kết quả.

### self argument
Chúng ta có một class `Employee`
```python
class Employee:
    def __init__(self, ID=None, department=None):
        self.ID = ID
        self.department = department
```
Khi chúng ta tạo object employee1
```python
employee1 = Employee("Puraudorin", "FAA")
```
Thì Python sẽ convert giúp chúng ta thành:
```Python
Employee.__init__(employee1, "Puraudorin", "FAA")
```
Và bên trong ``initializer`` sẽ thực thi như sau:
```
employee1.ID = "Puraudorin"
employee1.department = "FAA"
```


## Method overloading
> Overloading đề cập đến việc làm cho một method thực hiện các operations khác nhau dựa trên các **arguments** của nó.


Không như các ngôn ngữ lập trình khác, methods **không thể** explicitly overloaded ở Python, chỉ có thể implicitly overloaded.

![](overloading.png)


## Ví dụ:
```python
class Employee:
    # defining the properties and assigning them None to the
    def __init__(self, ID=None, salary=None, department=None):
        self.ID = ID
        self.salary = salary
        self.department = department

    # method overloading
    def demo(self, a, b, c, d=5, e=None):
        print("a =", a)
        print("b =", b)
        print("c =", c)
        print("d =", d)
        print("e =", e)
    def demo(self, a, b, c):
        print("a = ", a)
        print("b = ", b)
        print("c = ", c)
        

# cerating an object of the Employee class
Steve = Employee()

# Printing properties of Steve
print("Demo 1")
Steve.demo(1, 2, 3)
print("\n")

print("Demo 2")
Steve.demo(1, 2, 3, 4, 5)

```

**Output**
```
Demo 1
a =  1
b =  2
c =  3


Demo 2

Traceback (most recent call last):
  File "main.py", line 30, in <module>
    Steve.demo(1, 2, 3, 4, 5)
TypeError: demo() takes 4 positional arguments but 6 were given
```

Điều này là do chúng ta chỉ có thể sử dụng method được khai báo cuối cùng, ở đây là `demo` với 4 arguments (kể cả `self`).

Vậy phải làm sao? Chúng ta có vài cách để thực hiện method overloading trong Python, ở đây chúng ta sẽ dùng **multiple dispatch**

```python
from multipledispatch import dispatch

class Employee:
    # defining the properties and assigning them None to the
    def __init__(self, ID=None, salary=None, department=None):
        self.ID = ID
        self.salary = salary
        self.department = department

    @dispatch(int, int, int, int, int)
    def demo(self, a, b, c, d=5, e=None):
        print("a =", a)
        print("b =", b)
        print("c =", c)
        print("d =", d)
        print("e =", e)
        
    @dispatch(int, int, int)
    def demo(self, a, b, c):
        print("a = ", a)
        print("b = ", b)
        print("c = ", c)
        

# cerating an object of the Employee class
Steve = Employee()

# Printing properties of Steve
print("Demo 1")
Steve.demo(1, 2, 3)
print("\n")

print("Demo 2")
Steve.demo(1, 2, 3, 4, 5)
```
**Output**
```
Demo 1
a =  1
b =  2
c =  3


Demo 2
a = 1
b = 2
c = 3
d = 4
e = 5
```

## Class Method

**Class methods** làm việc với **class variables** và có thể truy cập bằng cách sử dụng `Class name`` thay vì object.
