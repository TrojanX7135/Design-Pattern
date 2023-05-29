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

- **Structural code in C#**

    Dưới đây là mẫu thiết kế Builder, trong đó các đối tượng phức tạp được tạo ra theo từng bước. Quá trình xây dựng có thể tạo ra các biểu diễn đối tượng khác nhau và cung cấp mức độ kiểm soát cao đối với việc lắp ráp các đối tượng.

```csharp

using System;
using System.Collections.Generic;

namespace DoFactory.GangOfFour.Builder.Structural
{
    /// <summary>
    /// MainApp startup class for Structural
    /// Builder Design Pattern.
    /// </summary>

    public class MainApp
    {
        /// <summary>
        /// Entry point into console application.
        /// </summary>

        public static void Main()
        {
            // Create director and builders

            Director director = new Director();

            Builder b1 = new ConcreteBuilder1();
            Builder b2 = new ConcreteBuilder2();

            // Construct two products

            director.Construct(b1);
            Product p1 = b1.GetResult();
            p1.Show();

            director.Construct(b2);
            Product p2 = b2.GetResult();
            p2.Show();

            // Wait for user

            Console.ReadKey();
        }
    }

    /// <summary>
    /// The 'Director' class
    /// </summary>

    class Director
    {
        // Builder uses a complex series of steps

        public void Construct(Builder builder)
        {
            builder.BuildPartA();
            builder.BuildPartB();
        }
    }

    /// <summary>
    /// The 'Builder' abstract class
    /// </summary>

    abstract class Builder
    {
        public abstract void BuildPartA();
        public abstract void BuildPartB();
        public abstract Product GetResult();
    }

    /// <summary>
    /// The 'ConcreteBuilder1' class
    /// </summary>

    class ConcreteBuilder1 : Builder
    {
        private Product _product = new Product();

        public override void BuildPartA()
        {
            _product.Add("PartA");
        }

        public override void BuildPartB()
        {
            _product.Add("PartB");
        }

        public override Product GetResult()
        {
            return _product;
        }
    }

    /// <summary>
    /// The 'ConcreteBuilder2' class
    /// </summary>

    class ConcreteBuilder2 : Builder
    {
        private Product _product = new Product();

        public override void BuildPartA()
        {
            _product.Add("PartX");
        }

        public override void BuildPartB()
        {
            _product.Add("PartY");
        }

        public override Product GetResult()
        {
            return _product;
        }
    }

    /// <summary>
    /// The 'Product' class
    /// </summary>

    class Product
    {
        private List<string> _parts = new List<string>();

        public void Add(string part)
        {
            _parts.Add(part);
        }

        public void Show()
        {
            Console.WriteLine("\nProduct Parts -------");
            foreach (string part in _parts)
                Console.WriteLine(part);
        }
    }
}



```

**Output**

```powershell
Product Parts -------
PartA
PartB

Product Parts -------
PartX
PartY
```

>    
> 
> * `MainApp` là lớp chạy chương trình, nó chứa phương thức `Main()` là điểm khởi đầu của ứng dụng console.
> * Trong phương thức `Main()`, ta tạo một `Director` và hai đối tượng `ConcreteBuilder1` và `ConcreteBuilder2`.
> * `Director` là lớp điều khiển quá trình xây dựng đối tượng. Nó sử dụng một chuỗi các bước phức tạp để xây dựng đối tượng theo từng bước.
> * `Builder` là lớp trừu tượng định nghĩa các phương thức để xây dựng các phần khác nhau của đối tượng.
> * `ConcreteBuilder1` và `ConcreteBuilder2` là hai lớp cụ thể kế thừa từ `Builder`. Chúng triển khai các phương thức xây dựng để tạo ra các phần khác nhau của đối tượng.
> * `Product` là lớp đại diện cho đối tượng cuối cùng được xây dựng. Nó có một danh sách các phần và các phương thức để thêm phần và hiển thị các phần của đối tượng.
> 
>     Trong phương thức `Main()`, chúng ta thực hiện xây dựng hai đối tượng `Product` sử dụng `Director` và `ConcreteBuilder1` và `ConcreteBuilder2`. Sau đó, chúng ta hiển thị các phần của các đối tượng bằng cách gọi phương thức `Show()` của `Product`.
> 
>     Điểm chính của mô hình Builder là tách rời quá trình xây dựng đối tượng khỏi việc tạo ra đối tượng, cho phép chúng ta xây dựng các đối tượng phức tạp từ các phần đơn giản một cách linh hoạt.



- **Real-world code in C#**

    Dưới đây là mẫu thiết kế Builder trong thế giới thực, trong đó các phương tiện khác nhau được lắp ráp theo từng bước. Cửa hàng sử dụng các VehicleBuilder để xây dựng nhiều loại phương tiện khác nhau theo một chuỗi các bước tuần tự.

```csharp
using System;
using System.Collections.Generic;

namespace DoFactory.GangOfFour.Builder.RealWorld
{
    /// <summary>
    /// MainApp startup class for Real-World 
    /// Builder Design Pattern.
    /// </summary>

    public class MainApp
    {
        /// <summary>
        /// Entry point into console application.
        /// </summary>

        public static void Main()
        {
            VehicleBuilder builder;

            // Create shop with vehicle builders

            Shop shop = new Shop();

            // Construct and display vehicles

            builder = new ScooterBuilder();
            shop.Construct(builder);
            builder.Vehicle.Show();

            builder = new CarBuilder();
            shop.Construct(builder);
            builder.Vehicle.Show();

            builder = new MotorCycleBuilder();
            shop.Construct(builder);
            builder.Vehicle.Show();

            // Wait for user

            Console.ReadKey();
        }
    }

    /// <summary>
    /// The 'Director' class
    /// </summary>

    class Shop
    {
        // Builder uses a complex series of steps

        public void Construct(VehicleBuilder vehicleBuilder)
        {
            vehicleBuilder.BuildFrame();
            vehicleBuilder.BuildEngine();
            vehicleBuilder.BuildWheels();
            vehicleBuilder.BuildDoors();
        }
    }

    /// <summary>
    /// The 'Builder' abstract class
    /// </summary>

    abstract class VehicleBuilder
    {
        protected Vehicle vehicle;

        // Gets vehicle instance

        public Vehicle Vehicle
        {
            get { return vehicle; }
        }

        // Abstract build methods

        public abstract void BuildFrame();
        public abstract void BuildEngine();
        public abstract void BuildWheels();
        public abstract void BuildDoors();
    }

    /// <summary>
    /// The 'ConcreteBuilder1' class
    /// </summary>

    class MotorCycleBuilder : VehicleBuilder
    {
        public MotorCycleBuilder()
        {
            vehicle = new Vehicle("MotorCycle");
        }

        public override void BuildFrame()
        {
            vehicle["frame"] = "MotorCycle Frame";
        }

        public override void BuildEngine()
        {
            vehicle["engine"] = "500 cc";
        }

        public override void BuildWheels()
        {
            vehicle["wheels"] = "2";
        }

        public override void BuildDoors()
        {
            vehicle["doors"] = "0";
        }
    }

    /// <summary>
    /// The 'ConcreteBuilder2' class
    /// </summary>

    class CarBuilder : VehicleBuilder
    {
        public CarBuilder()
        {
            vehicle = new Vehicle("Car");
        }

        public override void BuildFrame()
        {
            vehicle["frame"] = "Car Frame";
        }

        public override void BuildEngine()
        {
            vehicle["engine"] = "2500 cc";
        }

        public override void BuildWheels()
        {
            vehicle["wheels"] = "4";
        }

        public override void BuildDoors()
        {
            vehicle["doors"] = "4";
        }
    }

    /// <summary>
    /// The 'ConcreteBuilder3' class
    /// </summary>

    class ScooterBuilder : VehicleBuilder
    {
        public ScooterBuilder()
        {
            vehicle = new Vehicle("Scooter");
        }

        public override void BuildFrame()
        {
            vehicle["frame"] = "Scooter Frame";
        }

        public override void BuildEngine()
        {
            vehicle["engine"] = "50 cc";
        }

        public override void BuildWheels()
        {
            vehicle["wheels"] = "2";
        }

        public override void BuildDoors()
        {
            vehicle["doors"] = "0";
        }
    }

    /// <summary>
    /// The 'Product' class
    /// </summary>

    class Vehicle
    {
        private string _vehicleType;
        private Dictionary<string, string> _parts =
          new Dictionary<string, string>();

        // Constructor

        public Vehicle(string vehicleType)
        {
            this._vehicleType = vehicleType;
        }

        // Indexer

        public string this[string key]
        {
            get { return _parts[key]; }
            set { _parts[key] = value; }
        }

        public void Show()
        {
            Console.WriteLine("\n---------------------------");
            Console.WriteLine("Vehicle Type: {0}", _vehicleType);
            Console.WriteLine(" Frame : {0}", _parts["frame"]);
            Console.WriteLine(" Engine : {0}", _parts["engine"]);
            Console.WriteLine(" #Wheels: {0}", _parts["wheels"]);
            Console.WriteLine(" #Doors : {0}", _parts["doors"]);
        }
    }
}



```

**Output**

```powershell
---------------------------
Vehicle Type: Scooter
 Frame  : Scooter Frame
 Engine : none
 #Wheels: 2
 #Doors : 0

---------------------------
Vehicle Type: Car
 Frame  : Car Frame
 Engine : 2500 cc
 #Wheels: 4
 #Doors : 4

---------------------------
Vehicle Type: MotorCycle
 Frame  : MotorCycle Frame
 Engine : 500 cc
 #Wheels: 2
 #Doors : 0
```

>     
> 
> - Lớp `MainApp`: Là lớp khởi chạy ứng dụng console. Trong hàm `Main()`, nó tạo ra các đối tượng của các lớp xây dựng (Builder) và một đối tượng của lớp `Shop` để xây dựng và hiển thị các phương tiện giao thông.
> 
> - Lớp `Shop`: Đây là lớp "Director" trong mẫu thiết kế Builder. Nó quản lý quá trình xây dựng các phương tiện giao thông thông qua các bước xây dựng cụ thể được thực hiện bởi đối tượng lớp xây dựng (Builder). Phương thức `Construct()` của lớp Shop sẽ gọi lần lượt các phương thức xây dựng (Build) của lớp Builder.
> 
> - Lớp `VehicleBuilder` (Builder abstract class): Đây là lớp trừu tượng đại diện cho một Builder. Nó chứa một đối tượng `Vehicle` và định nghĩa các phương thức xây dựng (Build) trừu tượng cho các thành phần của phương tiện giao thông.
> 
> - Các lớp `ConcreteBuilder1`, `ConcreteBuilder2`, `ConcreteBuilder3` (Concrete Builder classes): Đây là các lớp cụ thể thừa kế từ `VehicleBuilder`. Mỗi lớp cụ thể này triển khai các phương thức xây dựng (Build) cụ thể cho mỗi thành phần của phương tiện giao thông như khung xe, động cơ, bánh xe và cửa.
> 
> - Lớp `Vehicle`: Đây là lớp "Product" đại diện cho phương tiện giao thông đã được xây dựng. Nó chứa các thành phần của phương tiện, được lưu trữ trong một từ điển (_parts), và cung cấp phương thức `Show()` để hiển thị thông tin về phương tiện.
> 
>     Khi chạy chương trình, nó sẽ tạo ra một đối tượng `Shop` và sử dụng các đối tượng `VehicleBuilder` cụ thể để xây dựng và hiển thị thông tin về các loại phương tiện giao thông như `Scooter`, `Car` và `MotorCycle`. Mỗi lớp `ConcreteBuilder` sẽ xây dựng các thành phần cụ thể cho phương tiện đó, và sau đó phương thức `Show()` của lớp `Vehicle` sẽ được gọi để hiển thị thông tin về phương tiện.







#### Thông tin thêm:

   Builder Pattern được xây dựng để khắc phục một số nhược điểm của Factory Pattern và Abstract Factory Pattern khi mà Object có nhiều thuộc tính. 

Có ba vấn đề chính với  Factory Pattern và Abstract Factory Pattern khi Object có nhiều thuộc tính:

* Quá nhiều tham số phải truyền vào từ phía client tới Factory Class.
* Một số tham số có thể là tùy chọn nhưng trong Factory Pattern, chúng ta phải gửi tất cả tham số, với tham số tùy chọn nếu không nhập gì thì sẽ truyền là null.
* Nếu một Object có quá nhiều thuộc tính thì việc tạo sẽ phức tạp.

Chúng ta có thể xử lý những vấn đề này với một số lượng lớn các tham số bằng việc cung cấp một hàm khởi tạo với những tham số bắt buộc và các method getter/ setter để cài đặt các tham số tùy chọn. Vấn đề với hướng tiếp cận này là trạng thái của Object sẽ không nhất quán cho tới khi tất cả các thuộc tính được cài đặt một cách rõ ràng. Nếu cần xây dựng một đối tượng Immutable thì cách này cũng không thể thực hiện được.
