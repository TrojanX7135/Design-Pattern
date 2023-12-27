# Facade Pattern

>     **Facade Pattern**  là một design pattern thuộc nhóm cấu trúc ( Structure Design Pattern ). 

---

<img title=" Facade Pattern cung cấp một giao diện chung thân thiện hơn để người dùng có thể dễ dàng sử dụng hệ thống con. Điều này giúp che giấu sự phức tạp của hệ thống con và làm cho nó dễ sử dụng hơn." src="https://images.viblo.asia/2ed6d10d-a495-4846-867b-854c50eb3a9d.png" alt="" data-align="center" style="zoom:100%;">

    Một ví dụ thực tế về việc sử dụng Facade Pattern có thể là khi bạn đến một khách sạn. Khi bạn đến khách sạn, bạn không cần phải liên hệ trực tiếp với từng bộ phận khác nhau của khách sạn để đặt phòng, đặt món ăn, yêu cầu dịch vụ giặt ủi,… Thay vào đó, bạn chỉ cần liên hệ với lễ tân và họ sẽ giúp bạn giải quyết tất cả các yêu cầu đó. Trong trường hợp này, lễ tân chính là một “Facade” giúp che giấu sự phức tạp của các bộ phận khác nhau trong khách sạn và cung cấp cho bạn một giao diện đơn giản để sử dụng các dịch vụ của khách sạn.

#### # Khái niệm :

>     **Facade Pattern** là một mẫu thiết kế thuộc nhóm cấu trúc
> 
>     Facade Pattern cung cấp cho chúng ta một giao diện chung đơn giản thay cho một nhóm các giao diện có trong một hệ thống con (subsystem). Facade Pattern định nghĩa một giao diện ở cấp độ cao hơn để giúp cho người dùng có thể dễ dàng sử dụng hệ thống con này.
> 
>     Facade Pattern cho phép các đối tượng truy cập trực tiếp giao diện chung này để giao tiếp với các giao diện có trong hệ thống con. Mục tiêu là che giấu các hoạt động phức tạp bên trong hệ thống con, làm cho hệ thống con dễ sử dụng hơn.

 

#### # Sơ đồ UML Facade Pattern :

<img title="UML Facade pattern" src="https://www.dofactory.com/img/diagrams/net/facade.png" alt="" data-align="center">

#### 

#### # Các thành phần:

Các lớp và đối tượng tham gia trong mẫu thiết kế này bao gồm:

* **Facade (MortgageApplication) :**
  
  * Biết rõ các lớp con hệ thống con nào chịu trách nhiệm cho một yêu cầu.
  
  * Chuyển giao yêu cầu của khách hàng cho các đối tượng hệ thống con thích hợp.

* **Subsystem classes (Bank, Credit, Loan) :**
  
  * Triển khai chức năng của hệ thống con.
  
  * Xử lý công việc được giao bởi đối tượng Facade.
  
  * Không biết về đối tượng facade và không giữ tham chiếu đến nó.
    
    

#### # Ta hãy đến với ví dụ :

- **Structural code in java**

    Đoạn Code cấu trúc này mô tả mẫu thiết kế Facade, cung cấp một giao diện đơn giản và đồng nhất cho một hệ thống con lớn gồm nhiều lớp.

```java
// 'Subsystem' classes
public class Engine {
    public void start() {
        System.out.println("Engine started");
    }
}

public class AirConditioner {
    public void start() {
        System.out.println("AirConditioner started");
    }
}

// 'Facade'
public class Car {
    private Engine engine;
    private AirConditioner airConditioner;

    public Car() {
        this.engine = new Engine();
        this.airConditioner = new AirConditioner();
    }

    public void start() {
        engine.start();
        airConditioner.start();
    }
}

// Chương trình chính để kiểm tra
public class Main {
    public static void main(String[] args) {
        Car car = new Car();
        car.start();
    }
}



```
