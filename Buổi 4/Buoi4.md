
- [Buổi 4: Mọi thứ đều là đối tượng](#buổi-4-mọi-thứ-đều-là-đối-tượng)
  - [I. Tính đóng gói (Encapsulation) trong Java](#i-tính-đóng-gói-encapsulation-trong-java)
      - [1. Tính đóng gói trong Java là gì?](#1-tính-đóng-gói-trong-java-là-gì)
      - [2. Tại sao cần tính đóng gói?](#2-tại-sao-cần-tính-đóng-gói)
  - [II. Tính kế thừa trong Java](#ii-tính-kế-thừa-trong-java)
      - [1. Tính kế thừa trong Java là gì?](#1-tính-kế-thừa-trong-java-là-gì)
      - [2. Tại sao lại dùng tính kế thừa trong Java?](#2-tại-sao-lại-dùng-tính-kế-thừa-trong-java)
      - [3. Cú pháp của tính kế thừa](#3-cú-pháp-của-tính-kế-thừa)
      - [4. Các loại kế thừa trong Java](#4-các-loại-kế-thừa-trong-java)
        - [Đơn kế thừa (Single Inheritance)](#đơn-kế-thừa-single-inheritance)
        - [Kế thừa đa cấp ((Multilevel inheritance))](#kế-thừa-đa-cấp-multilevel-inheritance)
        - [Kế thừa thứ bậc (Hierarchical Inheritance)](#kế-thừa-thứ-bậc-hierarchical-inheritance)
  - [III. Tính đa hình trong Java](#iii-tính-đa-hình-trong-java)
      - [1. Tính đa hình (Polymorphism) là gì?](#1-tính-đa-hình-polymorphism-là-gì)
        - [Tại sao cần tính đa hình?](#tại-sao-cần-tính-đa-hình)
      - [2. Tính đa hình lúc runtime trong Java](#2-tính-đa-hình-lúc-runtime-trong-java)
        - [Upcasting là gì?](#upcasting-là-gì)
        - [Downcasting là gì?](#downcasting-là-gì)
      - [Ví dụ về đa hình lúc runtime trong java](#ví-dụ-về-đa-hình-lúc-runtime-trong-java)
      - [3. Tính đa hình trong lúc biên dịch (compile)](#3-tính-đa-hình-trong-lúc-biên-dịch-compile)

# Buổi 4: Mọi thứ đều là đối tượng
## I. Tính đóng gói (Encapsulation) trong Java
#### 1. Tính đóng gói trong Java là gì?
- **Tính đóng gói (encapsulation)** là việc đóng gói các thuộc tính và phương thức bên trong lớp, tức là thiết kế để các thuộc tính và phương thức thuộc về (bên trong) một lớp.
- Với các **access modifier**, tính đóng gói sẽ có thể giúp ngăn chặn những lớp bên ngoài truy cập, thay đổi thuộc tính và phương thức của một lớp. Từ đó, giúp cho việc **che giấu dữ liệu** (data hiding).
- Để đạt được đóng gói trong Java chúng ta cần:
  - Khai báo các biến của một lớp là private.
  - Cung cấp phương thức setter và getter là public để có thể sửa đổi và xem các giá trị biến.
#### 2. Tại sao cần tính đóng gói?
- Trong lập trình, tính đóng gói giúp *bảo vệ dữ liệu* và *tránh truy cập trực tiếp* đến các thuộc tính của đối tượng từ bên ngoài. Điều này có ích trong việc quản lý và bảo vệ dữ liệu, đồng thời cho phép kiểm soát cách các thành phần khác nhau tương tác với đối tượng đó.
- VD về tính đóng gói:
``` java
public class Person {
    private String name;  // Thuộc tính name là private
    private int age;      // Thuộc tính age là private
    // Phương thức khởi tạo
    public Person(String name, int age) {
        this.name = name;
        this.age = age;
    }
    // Phương thức công khai để lấy tên
    public String getName() {
        return name;
    }
    // Phương thức công khai để lấy tuổi
    public int getAge() {
        return age;
    }
    // Phương thức công khai để thay đổi tuổi
    public void setAge(int age) {
        if (age >= 0) {
            this.age = age;
        }
    }
}
```
- Các phương thức public setAge(), getAge() và getName() là các điểm truy cập đến các biến của lớp Person (getters và setters). Vì vậy, bất kỳ đối tượng nào nào muốn truy cập vào các biến private sẽ truy cập chúng thông qua các trình getters và setters này.
- Lợi ích của đóng gói trong java
  - Tất cả các trường (field) của lớp có có chế độ chỉ đọc (**read-only**) hoặc chỉ ghi (**write-only**), tức là chỉ có hàm getter hoặc setter.
  - Một lớp có thể có toàn bộ điều khiển thông qua những gì được lưu giữ trong các trường (field) của nó.
  - Người sử dụng của class không biết cách các class lưu trữ dữ liệu. Một class có thể thay đổi kiểu dữ liệu của một trường và người dùng class không cần sự thay đổi trong code.
- Tính đóng gói là một nguyên tắc mạnh mẽ trong OOP, giúp tạo ra mã nguồn dễ bảo trì và an toàn hơn bằng cách quản lý truy cập đến thông tin của đối tượng.
## II. Tính kế thừa trong Java
#### 1. Tính kế thừa trong Java là gì?
- Tính kế thừa trong Java là một cơ chế trong đó một đối tượng có được tất cả các thuộc tính và hành vi của một đối tượng cha. 
- Ý tưởng đằng sau tính kế thừa trong Java là việc bạn có thể tạo các class mới được dựa trên các class đã có sẵn. Khi bạn kế thừa từ một class có sẵn, bạn có thể tái sử dụng các phương thức và trường của class cha. Hơn nữa, bạn có thể thêm các phương thức và trường mới trong class hiện tại.
- Tính kế thừa biểu diễn mối quan hệ IS-A, còn được gọi là mối quan hệ cha-con.
- Các thuật ngữ quan trọng trong kế thừa Java:
  - **Lớp cha (Superclass)**: Lớp mà các thuộc tính và phương thức được kế thừa bởi lớp con.
  - **Lớp con (Subclass)**: Lớp kế thừa các thuộc tính và phương thức từ lớp cha.
  - **extends**: Từ khóa  dùng để chỉ rõ lớp con kế thừa từ lớp cha.
  - **super**: Từ khóa dùng để truy cập các thuộc tính và phương thức của lớp cha từ lớp con.
#### 2. Tại sao lại dùng tính kế thừa trong Java?
- Có 1 số lý do vì sao nên dùng kế thừa trong lập trình Java:
  - Khả năng thể hiện các mối quan hệ kế thừa đảm bảo sự gần gũi với các mô hình trong thế giới thực.
  - Khả năng tái sử dụng. Khi dùng tính kế thừa ta có thể lấy 1 class mới từ 1 class hiện có và thêm tính năng mới vào nó mà không cần sửa đổi lớp cha và viết lại lớp cha để kế thừa nó.
  - Tính chất bắc cầu: Nếu lớp 1 kế thừa các thuộc tính từ 1 lớp B, sau đấy hầu hết các lớp con của A sẽ tự động kế thừa từ B. Tính chất này được gọi là tính chất bắc cầu của kế thừa.
#### 3. Cú pháp của tính kế thừa
- Để kế thừa 1 lớp, chúng ta dùng từ khóa **extends**. Cú pháp:
```java
class SubClass extends SuperClass{
// methods and fields
}
```
- VD về tính kế thừa trong Java:
![Alt text](image.png)
```java
class Employee {  
  float salary = 40000;  
}  

class Programmer extends Employee {  
  int bonus = 10000;
  public static void main(String args[]) {  
    Programmer p = new Programmer();
    System.out.println("Programmer salary is: " + p.salary);  
    System.out.println("Bonus of Programmer is: " + p.bonus);  
  }
}
```
Output:
```
Programmer salary is: 40000.0
Bonus of programmer is: 10000
```
- Ở trên, đối tượng Programmer có thể truy cập trường của riêng lớp nó cũng như của lớp Employee, đấy là ví dụ cho tính tái sử dụng.
#### 4. Các loại kế thừa trong Java
- Trên cơ sở class, có ba kiểu kế thừa trong Java: đơn kế thừa, kế thừa đa cấp, kế thừa thứ bậc.
![Alt text](image-1.png)

##### Đơn kế thừa (Single Inheritance)
- Đơn kế thừa: nghĩa là 1 lớp chỉ được kế thừa từ đúng 1 lớp khác. Hay nói cách khác, lớp con chỉ có duy nhất 1 lớp cha.
- VD: ở đây class Dog kế thừa class Animal
```java
class Animal {  
  void eat() {System.out.println("eating...");}  
} 

class Dog extends Animal {  
  void bark() {System.out.println("barking...");}  
}  

class Main {  
  public static void main(String args[]) {  
    Dog d = new Dog();
    d.bark();  
    d.eat();  
  }
}  
```
Output:
```
barking...
eating...
```
##### Kế thừa đa cấp ((Multilevel inheritance))
- Kế thừa đa cấp (multilevel inheritance) được sử dụng khi ta cần tạo ra các lớp con phức tạp và đa dạng, các lớp con này có thể kế thừa các thuộc tính và phương thức từ nhiều lớp cha khác nhau.
- Kế thừa đa cấp cho phép tạo ra một hệ thống kế thừa theo dạng đường thẳng, trong đó, một lớp được kế thừa từ một lớp cơ sở và cũng có thể đóng vai trò là lớp cơ sở cho các lớp khác.
- Kế thừa nhiều cấp là khi có một chuỗi kế thừa. Ở ví dụ dưới đây, BabyDog class kế thừa Dog class mà class này lại kế thừa Animal class, vì thế đây là kế thừa nhiều cấp.
- VD:
```java
class Animal {  
  void eat() {
    System.out.println("eating...");
  }  
} 
class Dog extends Animal {  
  void bark() {
    System.out.println("barking...");
  }  
}

class BabyDog extends Dog {  
  void weep() {
    System.out.println("weeping...");
  }  
}  

class TestInheritance2 {  
   public static void main(String args[]) {  
    BabyDog d = new BabyDog();
    d.weep();
    d.bark();  
    d.eat();  
  }
}  
```
Output:
```
weeping...
barking...
eating...
```
##### Kế thừa thứ bậc (Hierarchical Inheritance)
- 1 lớp cha được kế thừa bởi nhiều lớp con khác nhau. Hệ thống kế thừa trong Hierarchical inheritance có dạng cây. So với kế thừa đa cấp, trong kế thừa phân cấp, một lớp con có thể kế thừa từ một lớp cha và cũng là lớp cha của một lớp con khác, tạo ra một cây kế thừa phức tạp hơn.
- VD: các class Dog và Cat kế thừa Animal class, vì thế đây là kế thừa thứ bậc.
```java
class Animal {
  public void eat() {
    System.out.println(“Eating…”);
  }
}
class Dog extends Animal {
  public void bark() {
  System.out.println(“Barking…”);
  }
}
class Cat extends Animal {
  public void meow() {
  System.out.println(“Meowing…”);
  }
}
public class Main {
  public static void main(String[] args) {
    Dog d = new Dog();
    d.eat(); // gọi phương thức từ lớp cha
    d.bark(); // gọi phương thức từ lớp con
    Cat c = new Cat();
    c.eat(); // gọi phương thức từ lớp cha
    c.meow(); // gọi phương thức từ lớp con
  }
}
```
Output:
```
Eating...
Barking...
Eating...
Meowing...
``` 
## III. Tính đa hình trong Java
#### 1. Tính đa hình (Polymorphism) là gì?
- Tính đa hình (polymorphism) xuất phát từ tiếng Hy Lạp, có nghĩa là “nhiều hình dạng”, ý chỉ khả năng mà một đối tượng có thể nhận nhiều hình thức khác nhau. Ví dụ thực tế, cùng là một chiếc điện thoại, nhưng có thể sử dụng để gọi điện, nhắn tin, chụp ảnh, nghe nhạc... Đây chính là biểu hiện của tính đa hình.
- **Tính đa hình** là khả năng một đối tượng có thể thực hiện một tác vụ theo nhiều cách khác nhau. 
##### Tại sao cần tính đa hình?
- Tính đa hình giúp tạo ra mã nguồn linh hoạt và dễ bảo trì. Nó cho phép bạn viết các phương thức chung mà có thể được sử dụng trên nhiều lớp khác nhau, giúp giảm sự lặp lại mã và tạo ra mã nguồn dễ mở rộng.
- VD:
```java
// Lớp cha Shape
class Shape {
  void draw() {
    System.out.println("Vẽ hình...");
  }
  public static void main(String[] args) {
        Shape shape1 = new Circle();
        Shape shape2 = new Square();
        shape1.draw(); // gọi phương thức draw() của lớp Circle
        shape2.draw(); // gọi phương thức draw() của lớp Square
    }
}
// Lớp con Circle
class Circle extends Shape {
  void draw() {
    System.out.println("Vẽ hình tròn...");
  }
}
// Lớp con Square
class Square extends Shape {
  @Override
  void draw() {
    System.out.println("Vẽ hình vuông...");
  }
}

```
Output:
```
Vẽ hình tròn...
Vẽ hình vuông...
```
- Trong VD này, lớp cha Shape có một phương thức **draw()** mà các lớp con Circle và Square ghi đè (**Override**). Điều này có nghĩa là mỗi lớp con có cùng tên phương thức draw, nhưng chúng thực hiện hành động riêng biệt.

- Ưu điểm của tính đa hình:
  - Tái sử dụng mã nguồn: Bạn có thể sử dụng lại mã nguồn của các phương thức chung trên nhiều lớp con khác nhau.
  - Mã nguồn linh hoạt: Tính đa hình cho phép bạn thay đổi hành vi của các đối tượng mà không cần thay đổi mã nguồn của các lớp khác.
  - Tạo cấu trúc phân cấp: Bằng cách sử dụng tính đa hình, bạn có thể tạo ra các cấu trúc phân cấp cho các đối tượng trong ứng dụng của bạn, làm cho mã nguồn trở nên dễ bảo trì hơn.

- Trong Java, chúng ta sử dụng **nạp chồng phương thức** (method overloading) và **ghi đè phương thức** (method overriding) để có tính đa hình.
  - **Nạp chồng (Overloading)**: Đây là khả năng cho phép một lớp có nhiều thuộc tính, phương thức cùng tên nhưng với các tham số khác nhau về loại cũng như về số lượng. Khi được gọi, dựa vào tham số truyền vào, phương thức tương ứng sẽ được thực hiện.
  - **Ghi đè (Overriding)**: là hai phương thức cùng tên, cùng tham số, cùng kiểu trả về nhưng thằng con viết lại và dùng theo cách của nó, và xuất hiện ở lớp cha và tiếp tục xuất hiện ở lớp con. Khi dùng override, lúc thực thi, nếu lớp Con không có phương thức riêng, phương thức của lớp Cha sẽ được gọi, ngược lại nếu có, phương thức của lớp Con được gọi.

#### 2. Tính đa hình lúc runtime trong Java
- **Đa hình lúc runtime** là quá trình gọi phương thức đã được ghi đè trong thời gian thực thi chương trình. Trong quá trình này, một phương thức được ghi đè được gọi thông qua biến tham chiếu của một lớp cha.
> Lưu ý là quá trình quá trình ghi đè lúc runtime (hay overriding) chỉ xảy ra với các phương thức giống nhau về tham số và kiểu trả về. Các thuộc tính của đối tượng cha không thể bị ghi đè.
- Trước hết ta cần hiểu về **Upcasting** và **Downcasting**.
##### Upcasting là gì?
- Khi biến tham chiếu của lớp cha tham chiếu tới đối tượng của lớp con, thì đó là Upcasting.
```java
class Animal {
  public void eat() {
    System.out.println("eating...");
  }
}
public class Cat extends Animal {
    public void meow() {
        System.out.println("meowing...");
    }
}
```
```java
public class Upcasting {
    public static void main(String[] args) {
        Cat cat = new Cat();
        Animal animal1 = cat; // Chuyển kiểu không tường minh
        Animal animal2 = (Animal) cat; // Chuyển kiểu tường minh
        cat.eat();
        cat.meow();
        animal1.eat();
        animal2.eat();
        // animal2.meow(); // Không thể gọi phương thức meow()
    }
}
```
Output:
```
eating...
meowing...
eating...
eating...
```
- Với nội dung hàm main như trên, ta đã thực hiện upcasting khi gán đối tượng cat thuộc lớp Cat cho đối tượng animal1 và animal2 thuộc lớp Animal.
- Đối với upcasting, chúng ta hoàn toàn có thể sử dụng chuyển kiểu tường minh hoặc không tường minh, cả 2 cách đều được chấp nhận.
- Một lưu ý nhỏ: Mọi phương thức của lớp Animal hoàn toàn có thể gọi qua 1 đối tượng thuộc lớp Cat do giữa Animal và Cat có quan hệ IS_A (quan hệ cha con). Tuy nhiên, nếu thực hiện override bất kỳ phương thức nào của lớp Animal tại lớp Cat thì trong quá trình runtime hàm được gọi sẽ là hàm của lớp Cat .

##### Downcasting là gì?
- Khác với upcasting, **Downcasting** là dạng chuyển kiểu chuyển 1 đối tượng là một thể hiện của lớp cha xuống thành đối tượng là thể hiện của lớp con trong quan hệ kế thừa.
VD:
```java
public class Animal {
    public void eat() {
        System.out.println("eating...");
    }
}
```

```java
public class Cat extends Animal {
    public void meow() {
        System.out.println("meowing...");
    }
}

```

```java
public class Downcasting {
    public static void main(String[] args) {
        Animal animal = new Cat();
        Cat cat = (Cat) animal; // downcasting
        cat.meow();
    }

}
```

Output:
```
meowing...
```

#### Ví dụ về đa hình lúc runtime trong java
```java
public class Bike {
    public void run() {
        System.out.println("running");
    }
}
 
public class Splender extends Bike {
    public void run() {
        System.out.println("running safely with 60km");
    }
 
    public static void main(String args[]) {
        Bike b = new Splender(); // upcasting 
        b.run();
    }
}
```

#### 3. Tính đa hình trong lúc biên dịch (compile)
- Đa hình trong lúc biên dịch (compile): được sử dụng bằng cách **nạp chồng hàm (overloading).**
- Nạp chồng hàm:
Ta có thể sử dụng cùng một tên gọi cho các hàm "Giống nhau" (cùng mục đích) nhưng phải khác nhau về kiểu dữ liệu tham số hoặc số lượng tham số.
- Nạp chồng hàm cho phép ta khai báo và định nghĩa các hàm trên với cùng một tên gọi.
- Có 2 cách nạp chồng phương thức trong java
  - Thay đổi số lượng các tham số
  - Thay đổi kiểu dữ liệu của các tham số
- VD:
```java
public class Cong {
    public int cong(int a, int b) {
        return a + b;
    }
    public double cong(double a, double b) {
        return a + b;
    }
    public int cong(int a, int b, int c) {
        return a + b + c;
    }
}
```

```java
public class Main {
    public static void main(String[] args) {
        Cong cong = new Cong();
        System.out.println(cong.cong(3, 5));
        System.out.println(cong.cong(2.2, 3.3));
        System.out.println(cong.cong(2, 4, 5));
    }
}
```

Output:
```
8
5.5
11
```
