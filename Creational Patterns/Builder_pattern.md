# Builder Pattern

>     **Builder Pattern**  là một design pattern thuộc nhóm khởi tạo (Creational patterns).

---

<img title="Builder Pattern" src="https://ren0503.github.io/design-pattern/creational-pattern/builder/assets/intent.png" alt="" data-align="center" style="zoom:100%;">

    Ta có thể hình dung về Builder Pattern như việc xây dựng một ngôi nhà. Để xây dựng một ngôi nhà đơn giản, bạn cần xây dựng bốn bức tường và một sàn nhà, lắp đặt một cánh cửa, lắp đặt một cặp cửa sổ và xây dựng một mái nhà. Nhưng nếu bạn muốn một ngôi nhà rộng rãi hơn, sáng sủa hơn, với một sân sau và các tiện nghi khác ( như hệ thống sưởi ấm, ống nước và dây điện ) ? Mẫu thiết kế Builder đề xuất rằng bạn trích xuất mã xây dựng đối tượng ra khỏi lớp của nó và di chuyển nó sang các đối tượng riêng biệt được gọi là builders.

#### Khái niệm :

>     **Builder pattern** là một trong những **Creational pattern**. Builder pattern là mẫu thiết kế đối tượng được tạo ra để xây dựng một đối tượng phức tạp bằng cách sử dụng các đối tượng đơn giản và sử dụng tiếp cận từng bước, việc xây dựng các đối tượng đôc lập với các đối tượng khác.

 

#### Sơ đồ UML Builder Pattern :

<img title="UML builder pattern" src="https://www.dofactory.com/img/diagrams/net/builder.png" alt="" data-align="center">

#### Các thành phần:

Các lớp và đối tượng tham gia vào mẫu thiết kế này bao gồm:

* **Builder (VehicleBuilder) :**
  
  * Xác định một giao diện trừu tượng để tạo các phần của một đối tượng Sản phẩm.

* **ConcreteBuilder (MotorCycleBuilder, CarBuilder, ScooterBuilder) :**
  
  * Xây dựng và lắp ráp các phần của sản phẩm bằng cách triển khai giao diện Builder.
  
  * Xác định và theo dõi cách biểu diễn mà nó tạo ra.
  
  * Cung cấp một giao diện để lấy sản phẩm.

* **Director (Shop) :**
  
  * Xây dựng một đối tượng bằng cách sử dụng giao diện Builder.

* **Product (Vehicle) :**
  
  * Đại diện cho đối tượng phức tạp đang được xây dựng. ConcreteBuilder xây dựng biểu diễn nội bộ của sản phẩm và xác định quy trình để lắp ráp nó.
  * Bao gồm các lớp xác định các phần thành phần, bao gồm giao diện để lắp ráp các phần thành kết quả cuối cùng.
    
    

#### Ta hãy đến với ví dụ :

- **Structural code in java**

    Dưới đây là mẫu thiết kế Builder, trong đó các đối tượng phức tạp được tạo ra theo từng bước. Quá trình xây dựng có thể tạo ra các biểu diễn đối tượng khác nhau và cung cấp mức độ kiểm soát cao đối với việc lắp ráp các đối tượng.

```java

// Lớp "Product"
class Car {
    private String make;
    private String model;
    private int year;

    public void setMake(String make) { this.make = make; }
    public void setModel(String model) { this.model = model; }
    public void setYear(int year) { this.year = year; }

    @Override
    public String toString() {
        return "Car [make=" + make + ", model=" + model + ", year=" + year + "]";
    }
}

// "Builder" interface
interface CarBuilder {
    void buildMake();
    void buildModel();
    void buildYear();
    Car getCar();
}

// "ConcreteBuilder"
class SedanCarBuilder implements CarBuilder {
    private Car car;

    public SedanCarBuilder() {
        this.car = new Car();
    }

    @Override
    public void buildMake() {
        car.setMake("Sedan");
    }

    @Override
    public void buildModel() {
        car.setModel("Honda City");
    }

    @Override
    public void buildYear() {
        car.setYear(2021);
    }

    @Override
    public Car getCar() {
        return this.car;
    }
}

// "Director"
class CarDirector {
    private CarBuilder carBuilder;

    public CarDirector(CarBuilder carBuilder) {
        this.carBuilder = carBuilder;
    }

    public void buildCar() {
        carBuilder.buildMake();
        carBuilder.buildModel();
        carBuilder.buildYear();
    }

    public Car getCar() {
        return this.carBuilder.getCar();
    }
}

// Sử dụng Builder
public class BuilderPatternExample {
    public static void main(String[] args) {
        CarBuilder builder = new SedanCarBuilder();
        CarDirector director = new CarDirector(builder);
        director.buildCar();
        Car car = director.getCar();
        System.out.println(car);
    }
}




```

**Output**

```powershell
Car [make=Sedan, model=Honda City, year=2021]
```

Trong ví dụ này, Car là lớp `Product`, CarBuilder là `Builder` interface, SedanCarBuilder là `ConcreteBuilder`, và CarDirector là `Director`. Mẫu thiết kế Builder giúp tạo ra một đối tượng phức tạp bằng cách chỉ định các bước tạo lập thông qua một `Builder` interface, sau đó cho phép một `Director` điều khiển quá trình tạo lập. Điều này giúp tách rời quá trình xây dựng một đối tượng phức tạp khỏi các phần tử cấu thành nó, cho phép cùng một quá trình xây dựng có thể tạo ra các đối tượng khác nhau. Trong ví dụ này, bạn có thể thêm nhiều `ConcreteBuilder` khác nhau để tạo ra các loại Car khác nhau.



`?` **Nếu không dùng builder Design Pattern thì sẽ như thế nào**

```java

// Lớp "Product"
class Car {
    private String make;
    private String model;
    private int year;

    public void setMake(String make) { this.make = make; }
    public void setModel(String model) { this.model = model; }
    public void setYear(int year) { this.year = year; }

    @Override
    public String toString() {
        return "Car [make=" + make + ", model=" + model + ", year=" + year + "]";
    }
}

// Sử dụng Car
public class Main {
    public static void main(String[] args) {
        // Tạo một đối tượng Car
        Car car = new Car();

        // Thiết lập các thuộc tính của Car
        car.setMake("Sedan");
        car.setModel("Honda City");
        car.setYear(2021);

        // In ra thông tin của Car
        System.out.println(car);
    }
}


```

Trong ví dụ trên, chúng ta tạo một đối tượng `Car` mới và thiết lập các thuộc tính của nó bằng cách gọi các phương thức `setter`. Điều này tạo ra một đối tượng `Car` với các thuộc tính giống như khi sử dụng mẫu thiết kế `Builder`, nhưng không cần phải tạo và sử dụng các lớp `CarBuilder`, `SedanCarBuilder`, và `CarDirector`. Tuy nhiên, nếu việc tạo một đối tượng `Car` đòi hỏi nhiều bước phức tạp và/hoặc cần phải tạo ra nhiều loại `Car` khác nhau, việc sử dụng mẫu thiết kế `Builder` có thể giúp làm cho mã nguồn dễ đọc, dễ bảo dưỡng, và linh hoạt hơn. Mẫu thiết kế `Builder` cũng giúp tách rời quá trình xây dựng một đối tượng phức tạp khỏi các phần tử cấu thành nó, cho phép cùng một quá trình xây dựng có thể tạo ra các đối tượng khác nhau. Trong ví dụ này, bạn có thể thêm nhiều `ConcreteBuilder` khác nhau để tạo ra các loại `Car` khác nhau.


#### Thông tin thêm:

   Builder Pattern được xây dựng để khắc phục một số nhược điểm của Factory Pattern và Abstract Factory Pattern khi mà Object có nhiều thuộc tính. 

Có ba vấn đề chính với  Factory Pattern và Abstract Factory Pattern khi Object có nhiều thuộc tính:

* Quá nhiều tham số phải truyền vào từ phía client tới Factory Class.
* Một số tham số có thể là tùy chọn nhưng trong Factory Pattern, chúng ta phải gửi tất cả tham số, với tham số tùy chọn nếu không nhập gì thì sẽ truyền là null.
* Nếu một Object có quá nhiều thuộc tính thì việc tạo sẽ phức tạp.

Chúng ta có thể xử lý những vấn đề này với một số lượng lớn các tham số bằng việc cung cấp một hàm khởi tạo với những tham số bắt buộc và các method getter/ setter để cài đặt các tham số tùy chọn. Vấn đề với hướng tiếp cận này là trạng thái của Object sẽ không nhất quán cho tới khi tất cả các thuộc tính được cài đặt một cách rõ ràng. Nếu cần xây dựng một đối tượng Immutable thì cách này cũng không thể thực hiện được.
