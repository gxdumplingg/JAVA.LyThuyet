- [\[Buổi 7\] Interface và trừu tượng](#buổi-7-interface-và-trừu-tượng)
  - [1. Tính trừu tượng là gì?](#1-tính-trừu-tượng-là-gì)
  - [2. Lớp trừu tượng](#2-lớp-trừu-tượng)
      - [Phương thức trừu tượng Abstract trong Java](#phương-thức-trừu-tượng-abstract-trong-java)
  - [3. Interface là gì?](#3-interface-là-gì)
      - [Triển khai interface](#triển-khai-interface)
      - [Đa kế thừa trong Java bởi Interface](#đa-kế-thừa-trong-java-bởi-interface)
  - [4. Sự khác nhau giữa Interface và Abstract Class](#4-sự-khác-nhau-giữa-interface-và-abstract-class)
      - [Khi nào sử dụng Abstract Class và Interface?](#khi-nào-sử-dụng-abstract-class-và-interface)

# [Buổi 7] Interface và trừu tượng

## 1. Tính trừu tượng là gì?
- Tính trừu tượng là một tiến trình ẩn các chi tiết trình triển khai và chỉ hiển thị tính năng tới người dùng. Tính trừu tượng cho phép loại bỏ tính chất phức tạp của đối tượng bằng cách chỉ đưa ra các thuộc tính và phương thức cần thiết của đối tượng trong lập trình.
- Tính trừu tượng giúp tập trung vào những cốt lõi cần thiết của đối tượng thay vì quan tâm đến cách nó thực hiện.
- Trong Java, chúng tà sử dụng **abstract class** và **abstract interface** để có tính trừu tượng.
## 2. Lớp trừu tượng
- Một lớp được khai báo với từ khóa **abstract** là lớp trừu tượng (abstract class).
- Lớp trừu tượng có thể có các phương thức abstract hoặc non-abtract.
- Lớp trừu tượng có thể khai báo 0, 1 hoặc nhiều method trừu tượng bên trong.
- Không thể khởi tạo 1 đối tượng trực tiếp từ một class trừu tượng.
- Abstraction Class không thể khởi tạo tham số mà chỉ khai báo, nó được dùng như 1 **lớp cha** của các lớp có cùng bản chất như kiểu, loại, nhiệm vụ.
- 1 lớp kế thừa từ lớp trừu tượng không cần phải implement non-abstract methods, nhưng những method nào có abstract thì bắt buộc phải **override**, trừ khi subclass cũng là abstract.
- Syntax:
```java
abstract class NameClass{
// class body
}
```
#### Phương thức trừu tượng Abstract trong Java
- 1 phương thức được khai báo là `abstract` và không có tính triển khai thì đó là **phương thức trừu tượng**. Phương thức sẽ được triển khai trog các lớp con.
- Cũng giống như lớp thông thường, lớp trừu tượng có thể có cả phương thức abstract và non-abstract. Ví dụ:
``` java
public abstract class Polygon {
    // abstract method 
    public abstract void getArea();
    // non-abstract method
    public void printSides() {
        System.out.println("Print sides of Polygon.");
    }
}
```
- Chúng ta không thể tạo các đối tượng của lớp trừu tượng, vậy làm thế nào để truy cập các phương thức bên trong lớp? Trong Java, chúng ta phải kế thừa lớp trừu tượng để sử dụng nó. Ví dụ:
```java
public abstract class Polygon {
    // abstract method 
    abstract void getArea();
    // non-abstract method
    public void printSides() {
        System.out.println("Print sides of Polygon.");
    }
}
public class Rectangle extends Polygon {
    // implementation of abstract method
    void getArea() {
        System.out.println("Print the area of Polygon.");
    }
}
class Main {
    public static void main(String[] args) {
        // create object of the child class
        Rectangle rectangle1 = new Rectangle();
        // access the non-abstract method
        rectangle1.printSides();
        // access the implemented abstract method
        rectangle1.getArea();
    }
}
```
Output: 
```
Print sides of Polygon.
Print the area of Polygon.
```
- Trong ví dụ trên, chúng ta đã tạo lớp `Rectangle` bằng cách kế thừa lớp trừu tượng `Polygon`.
- Lớp `Rectangle` hiện kế thừa cả phương thức trừu tượng và không trừu tượng. Chúng ta phải cung cấp triển khai cho phương thức trừu tượng `getArea()`.
- Sau đó ta sử dụng đối tượng `Rectangle` để truy cập các phương thức của lớp trừu tượng.
## 3. Interface là gì?
- Một `interface` không phải là một lớp. Viết một interface giống như viết một lớp, nhưng chúng có 2 định nghĩa khác nhau. Trong khi lớp mô tả các thuộc tính và hành vi của một đối tượng, thì interface chứa các hành vi mà một class triển khai, nó chỉ có **phương thức trừu tượng và các hằng số**.
- Trừ khi một lớp triển khai interface là lớp trừu tượng abstract, còn lại tất cả các phương thức của interface cần được định nghĩa trong class. 
- Tất cả các hằng số đều được mặc định ở dạng **public static final**.
- Tất cả các phương thức đều ở dạng **public**.
- Interface không có hàm khởi tạo (constructor).
- Tương tự lớp abstract, nó **không thể được khởi tạo thành 1 đối tượng**.
- Trong Java, chúng ta sử dụng từ khóa `interface` để tạo 1 interface. VD:
```java
interface Animal{ // chỉ chứa các phương thức trừu tượng
  abstract public void play(); 
  abstract public void makeSound();
}
```
#### Triển khai interface
- Cũng giống như lớp trừu tượng, chúng ta không thể tạo các đối tượng của interface. Để sử dụng interface, các lớp khác phải triển khai interface đó.

- Chúng ta sử dụng từ khóa `implements` để triển khai interface. Ví dụ:
```java
interface Animal {
    abstract public void play(); 
    abstract public void makeSound();
}
 
class Dog implements Animal {
    // implement play()
    public void play() {
        System.out.println("Play ball");
    }
    // implement makeSound()
    public void makeSound() {
        System.out.println("Woof Woof");
    }
}
class Main {
   public static void main(String[] args) {
       // object of Dog
       Dog dog = new Dog();
      
       // access abstract methods
       dog.play();
       dog.makeSound();
   }
}
```
Output:
```
Play ball
Woof Woof
```
- Khi triển khai `interface`:
  - Một lớp có thể triển khai một hoặc nhiều interface tại một thời điểm.
  - Một lớp chỉ có thể kế thừa một lớp khác, nhưng được triển khai nhiều interface.
  - Một interface có thể kế thừa từ một interface khác, tương tự cách một lớp có thể kế thừa lớp khác.
#### Đa kế thừa trong Java bởi Interface
- Nếu một lớp triển khai (implements) nhiều interface, hoặc một Interface kế thừa từ nhiều Interface khác thì đó là đa kế thừa.
- Trong Java, một `class` chỉ được thừa kế (`extends`) từ một class và có thể cài đặt (`implements`) nhiều interface. Tuy nhiên, một `interface` có thể thừa kế (`extends`) nhiều interface.

- Một `interface` không thể cài đặt (`implements`) interface khác, do interface không chứa phần cài đặt, chỉ chứa các khai báo.
- VD về 1 class implements nhiều interface:
```java
public interface Shape {    
    void draw();    
}
public interface Color {
    String getColor();
}
public class Rectangle implements Shape, Color {
    @Override
    public void draw() {
        System.out.println("Draw " + this.getColor() + " rectangle");
    }
    @Override
    public String getColor() {
        return "red";
    }
}
```
- VD interface `extends` interface khác:
```java
interface Printable{
    void print();
}
interface Showable extends Printable{
    void show();
}
class A3 implements Showable{
    public void print() {
        System.out.println("In");
    }
    public void show() {
        System.out.println("Hiển thị");
    }
    public static void main(String args[]){
        A3 obj = new A3();
        obj.print();
        obj.show();
    }
}
```
- VD về đa kế thừa trong Java bởi Interface:
```java
interface Printable {
    void print();
}
interface Showable{
    void show();
}
class A4 implements Printable, Showable {
    public void print() {
        System.out.println("In");
    }
    public void show() {
        System.out.println("Hiển thị");
    }
    public static void main(String args[]){
        A4 obj = new A4();
        obj.print();
        obj.show();
    }
}
```
## 4. Sự khác nhau giữa Interface và Abstract Class
|Abstract Class   |Interface     |
|---|---|
| Thể hiện tính trừu tượng < 100%  |Thể hiện tính trừu tượng 100% (`Java<8`).  |
|Có thể có các phương thức abstract và non-abstract|- Phiên bản `Java < 8`, Interface chỉ có thể có phương thức `abstract`; `Java 8`, có thể thêm `default` và `static methods`; `Java 9`, có thể thêm `private methods`.|
|Không hỗ trợ đa kế thừa|Hỗ trợ **đa kế thừa**|
|Có thể có các biến **final**, **non-final**, **static** và **non-static**|Chỉ có các biến **static final**|
|Có thể định nghĩa thân phương thức, property.|Không thể định nghĩa code xử lý, chỉ có thể khai báo.|
|Có thể có phương thức **static**, phương thức **main** và **constructor**|Không thể có phương thức **static**, **main** hoặc **constructor**.|
|Từ khóa `abstract` được sử dụng để khai báo lớp trừu tượng|Từ khóa `interface` được sử dụng để khai báo Interface|
|Không cần thiết|Mọi phương thức, property của interface cần được hiện thực trong class.|
 
#### Khi nào sử dụng Abstract Class và Interface?
- Interface : Sử dụng Interface khi bạn muốn tạo dựng một bộ khung chuẩn gồm các chức năng (method/ function) mà tất cả module/ project cần phải có.

- Abstract class: Khi chúng ta chỉ có thể hoàn thành một vài chức năng (method/ function) chuẩn của hệ thống, một vài chức năng còn lại các lớp extends phải hoàn thành. VD 1 đối tượng có những chức năng A,B,C trong đó tính năng A,B chắc chắn sẽ thực thi theo cách nào đó, còn tính năng C phải tùy thuộc vào đối tượng cụ thể là gì, như đối tượng Dog, Cat tuy chúng đều có thể phát ra âm thanh nhưng âm thanh là khác nhau. Vì vậy method Speak() là `abstract method` để chỉ ra rằng tính năng này còn dang dở chưa rõ thực thi, các lớp `extends` phải hoàn thành nốt tính năng này, còn những tính năng đã hoàn thành vẫn sử dụng như bình thường đây là những tính năng chung.

