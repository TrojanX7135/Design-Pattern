# Command Pattern

>    **Command Pattern** (hay còn gọi là Action, Transaction) là một mẫu thiết kế thuộc nhóm hành vi (Behavioral Pattern).

---

<img title="Người ra lệnh cần cung cấp một class đóng gói những mệnh lệnh. Người nhận mệnh lệnh cần phân biệt những interface nào để thực hiện đúng mệnh lệnh." src="https://refactoring.guru/images/patterns/content/command/command-en.png" alt="" data-align="center" style="zoom:100%;">

   Một ví dụ thực tế về Command pattern, trong một nhà hàng ta có người phục vụ và đầu bếp. Người phục vụ sẽ nhận đơn hàng từ khách hàng và chuyển đến cho đầu bếp. 

    Trong ví dụ này, Command pattern có thể được áp dụng để đóng gói yêu cầu đặt món ăn của khách hàng thành một object Command. Người phục vụ sẽ nhận yêu cầu đặt món ăn từ khách hàng và chuyển đến cho đầu bếp thông qua object Command. Đầu bếp sẽ nhận object Command và thực hiện yêu cầu đặt món ăn của khách hàng.

#### # Khái niệm :

>     **Command pattern** là một pattern cho phép bạn chuyển đổi một request thành một object độc lập chứa tất cả thông tin về request. Việc chuyển đổi này cho phép bạn tham số hoá các methods với các yêu cầu khác nhau như log, queue (undo/redo), transtraction.
> 
>     Khái niệm Command Object ( đối tượng ) giống như một class trung gian được tạo ra để lưu trữ các câu lệnh và trạng thái của object tại một thời điểm nào đó.
> 
>     Command dịch ra nghĩa là ra lệnh. Commander nghĩa là chỉ huy, người này không làm mà chỉ ra lệnh cho người khác làm. Như vậy, phải có người nhận lệnh và thi hành lệnh. Người ra lệnh cần cung cấp một class đóng gói những mệnh lệnh. Người nhận mệnh lệnh cần phân biệt những interface nào để thực hiện đúng mệnh lệnh.

 

#### # Sơ đồ UML Command Pattern :

<img title="UML Command pattern" src="https://www.dofactory.com/img/diagrams/net/command.png" alt="" data-align="center">

#### # Các thành phần :

Các lớp và đối tượng tham gia trong mẫu thiết kế này bao gồm:

* **Command (Command) :**
  
  * Khai báo một giao diện để thực hiện một hoạt động.

* **ConcreteCommand (CalculatorCommand) :**
  
  * Xác định một liên kết giữa đối tượng Receiver và một hành động.
  * Triển khai Execute bằng cách gọi các hoạt động tương ứng trên Receiver.

* **Client (CommandApp) :**
  
  * Tạo một đối tượng ConcreteCommand và thiết lập Receiver của nó.
  
  Invoker (User)
  
  * Yêu cầu command thực hiện yêu cầu.

* **Receiver (Calculator) :**
  
  * Biết cách thực hiện các hoạt động liên quan đến việc thực hiện yêu cầu.
  
  

#### # Ta hãy đến với ví dụ :

- **Structural code in java**

    Đoạn Code này mô tả mẫu thiết kế Command.

```java

// Interface 'Command'
public interface Command {
    void execute();
}

// Lớp 'Receiver'
public class Light {
    public void on() {
        System.out.println("The light is on");
    }

    public void off() {
        System.out.println("The light is off");
    }
}

// Lớp 'ConcreteCommand'
public class LightOnCommand implements Command {
    private Light light;

    public LightOnCommand(Light light) {
        this.light = light;
    }

    public void execute() {
        light.on();
    }
}

public class LightOffCommand implements Command {
    private Light light;

    public LightOffCommand(Light light) {
        this.light = light;
    }

    public void execute() {
        light.off();
    }
}

// Lớp 'Invoker'
public class RemoteControl {
    private Command command;

    public void setCommand(Command command) {
        this.command = command;
    }

    public void pressButton() {
        command.execute();
    }
}

// Chương trình chính để kiểm tra
public class Main {
    public static void main(String[] args) {
        Light light = new Light();
        Command lightOn = new LightOnCommand(light);
        Command lightOff = new LightOffCommand(light);

        RemoteControl control = new RemoteControl();

        // Bật đèn
        control.setCommand(lightOn);
        control.pressButton();

        // Tắt đèn
        control.setCommand(lightOff);
        control.pressButton();
    }
}

```

