# Adapter Pattern

>     **Adapter Pattern**  là một design pattern thuộc nhóm cấu trúc ( Structure Design Pattern ).
> 
>     **Vậy tại sao nó lại thuộc nhóm cấu trúc ?**
> 
>     Adapter pattern thuộc vào nhóm structural design pattern vì nó giải quyết các vấn đề liên quan đến cấu trúc của các đối tượng và lớp trong một ứng dụng. Mục tiêu chính của Adapter pattern là tạo một giao diện thích hợp để kết nối hai thành phần có giao diện không tương thích với nhau.

---

<img title="Adapter Pattern giúp cái xe ô tô (4 bánh không phải loại chạy xe lửa), thông qua dăm ba cái khúc gỗ trục xoay quỷ ma gì đó thì có thể chạy trên đường ray. Hợp lí." src="https://refactoring.guru/images/patterns/content/adapter/adapter-en-3x.png" alt="" data-align="center" style="zoom:33%;">

    Một ví dụ thực tế của Adapter pattern là khi bạn đi du lịch từ Mỹ sang châu Âu lần đầu tiên, bạn có thể bị ngạc nhiên khi cố gắng sạc laptop của mình. Tiêu chuẩn ổ cắm và phích cắm điện là khác nhau ở các quốc gia khác nhau. Phích cắm ở Mỹ sẽ có 2 chấu thay vì ở Châu Âu là 3 chấu hoặc khoảng cách phích cắm to hơn. Vấn đề này có thể được giải quyết bằng cách sử dụng một bộ chuyển đổi phích cắm điện có ổ cắm kiểu Mỹ và phích cắm kiểu châu Âu.

    Trong lập trình, Adapter pattern hoạt động tương tự như vậy bằng cách giới thiệu một lớp adapter bổ sung giữa một giao diện và một lớp hiện có. Lớp adapter thực hiện giao diện mong đợi và giữ một tham chiếu đến một đối tượng của lớp bạn muốn sử dụng lại.

=> Tóm lại: Adapter Pattern đơn giản là để hai thằng objects có interface khác nhau có thể work được với nhau.

#### # Khái niệm :

>     **Apdapter pattern** là một mẫu thiết kế cấu trúc cho phép các đối tượng có interface không tương thích cộng tác với nhau.
> 
>     Khi bạn có hai đối tượng hoặc lớp với giao diện không tương thích, Adapter pattern giúp bạn tạo ra một adapter (bộ chuyển đổi) để chuyển đổi giao diện của một đối tượng thành giao diện mà đối tượng khác có thể sử dụng. Adapter này cung cấp một lớp trung gian giữa hai giao diện không tương thích và cung cấp phương thức để chuyển đổi và giao tiếp giữa chúng.

 

#### # Mục đích ra đời :

    Ví dụ về một project có 2 ông dev làm 2 module khác nhau, ông A sẽ call một cái function nào đó bên module của ông B, nhưng ổng sẽ gọi theo một cái interface mà ổng tự đặt ra không cần quan tâm tới ông B ổng đặt cái interface đó là gì...



Đây là cách nó hoạt động:

* Adapter có một interface tương thích với một trong các object hiện có.
* Với việc sử dụng interface này, object hiện có có thể gọi các phương thức của Adapter một cách an toàn.
* Khi được gọi, Adapter sẽ chuyển yêu cầu đến object thứ hai, nhưng theo một định dạng và thứ tự mà object thứ hai mong đợi.

#### # Sơ đồ UML Adapter Pattern :

<img title="UML Adapter pattern" src="https://www.dofactory.com/img/diagrams/net/adapter.png" alt="" data-align="center">

#### 

#### 

#### # Các thành phần:

Các lớp và đối tượng tham gia trong mẫu thiết kế này bao gồm:

* **Target (ChemicalCompound) :** Giao diện mà Client muốn sử dụng.

* **Adapter (Compound) :** Lớp adapter chuyển đổi giao diện cũ của đối tượng thành giao diện mới theo yêu cầu của Target.

* **Adaptee (ChemicalDatabank) :** Đối tượng có giao diện không tương thích với Target.

* **Client (AdapterApp) :** Đối tượng sử dụng Target để tương tác với Adaptee thông qua Adapter.
  
  

#### # Ta hãy đến với ví dụ :

- **Structural code in java**

    Đoạn mã này mô tả mẫu thiết kế Adapter, giúp ánh xạ giao diện của một lớp vào một lớp khác để chúng có thể hoạt động cùng nhau. Các lớp không tương thích này có thể đến từ các thư viện hoặc khung công việc khác nhau.

```java

public class Main {
    public static void main(String[] args) {
        // Khởi tạo một đối tượng Adapter và gọi phương thức request()
        Target target = new Adapter();
        target.request();
    }
}

// Class Target định nghĩa interface mà client sử dụng
class Target {
    public void request() {
        System.out.println("Called Target request()"); // yêu cầu mà Target gọi
    }
}

// Class Adapter kế thừa từ class Target và chứa một đối tượng Adaptee
class Adapter extends Target {
    private Adaptee adaptee = new Adaptee();

    @Override
    public void request() {
        // gọi phương thức specificRequest()
        adaptee.specificRequest();
    }
}

// Class Adaptee chứa một phương thức specificRequest()
class Adaptee {
    public void specificRequest() {
        System.out.println("Called SpecificRequest()"); // yêu cầu cụ thể nằm bên adaptee
    }
}


```

**Output**

```powershell
Called SpecificRequest()
```

>     Trong đó:
> 
> * `Program` là class chứa hàm `Main` để chạy chương trình.
> 
> * `Target` là class định nghĩa interface mà client sử dụng. Nó có một phương thức ảo `Request()` để hiển thị thông báo “Called Target Request()”.
> 
> * `Adapter` là class kế thừa từ `Target` và chứa một đối tượng `Adaptee`. Nó ghi đè phương thức `Request()` để gọi phương thức `SpecificRequest()` của đối tượng `Adaptee`.
> 
> * `Adaptee` là class chứa một phương thức `SpecificRequest()` để hiển thị thông báo “Called SpecificRequest()”.
> 
> Khi chạy chương trình, hàm `Main` sẽ khởi tạo một đối tượng `Adapter` và gọi phương thức `Request()` của nó. Phương thức này sẽ gọi phương thức `SpecificRequest()` của đối tượng `Adaptee`, và kết quả là hiển thị thông báo `Called SpecificRequest()`.
> 
> `client` được xem là hàm `Main` trong class `Program`. Hàm `Main` sử dụng interface của class `Target` thông qua đối tượng `Adapter` mà nó khởi tạo và gọi phương thức `Request()` của đối tượng đó.



- **Real-world code in java**

```java
// Đầu tiên, chúng ta có một interface mục tiêu (Target interface)
public interface VietnameseSocket {
    public void provideElectricity();
}

// Tiếp theo, chúng ta có một lớp cần thích ứng (Adaptee class)
public class AmericanSocket {
    public void provideElectricity() {
        System.out.println("Providing electricity with American standard");
    }
}

// Cuối cùng, chúng ta tạo ra một Adapter để kết nối hai interface không tương thích
public class Adapter implements VietnameseSocket {
    private AmericanSocket americanSocket;

    public Adapter(AmericanSocket americanSocket) {
        this.americanSocket = americanSocket;
    }

    @Override
    public void provideElectricity() {
        americanSocket.provideElectricity();
    }
}


```



