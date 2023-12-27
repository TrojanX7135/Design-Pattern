# Abstract Factory Pattern

>     **Abstract Factory Pattern**  là một design pattern thuộc nhóm khởi tạo (Creational patterns).

---

<img title="Abstract Factory Pattern" src="https://refactoring.guru/images/patterns/content/abstract-factory/abstract-factory-en-3x.png" alt="" data-align="center" style="zoom:33%;">

    Nó có thể được hình dung như một nhà máy lớn, bên trong có các nhà máy nhỏ hơn sản xuất ra những loạt sản phẩm liên quan đến nhau.

    Hãy lấy một nhà máy nội thất làm ví dụ. Họ có các bộ bàn ghế theo từng concept khác nhau, nên họ phân ra các nhà máy riêng biệt chế tạo các bộ bàn ghế theo concept riêng biệt. Vd: Spheric Factory chế tạo các bộ bàn ghế ghế theo concept hình cầu, Pyramidal Factory chế tạo các bộ bàn ghế kiểu tam giác,...

#### Khái niệm :

>     Abstract Factory là một mẫu thiết kế khởi tạo ( creational desgin pattern ) cho phép bạn tạo ra các gia đình của các đối tượng liên quan mà không cần chỉ định các lớp cụ thể của chúng.
> 
>     Mẫu này cung cấp một cách để tạo ra các gia đình của các đối tượng liên quan mà không áp đặt các lớp cụ thể của chúng, bằng cách đóng gói một nhóm các nhà máy cá nhân có chủ đề chung mà không chỉ định các lớp cụ thể của chúng.

 

#### Ta hãy đến với ví dụ :

    đây là ví dụ về một cửa hàng nội thất có 2 concept nội thất là Spheric và Pyramidal :

```java

public interface IChair {
    void sitOn();
}

public interface ISofa {
    void sitOn();
}

public interface ICoffeeTable {
    void putOn();
}

public interface IFurnitureFactory {
    IChair createChair();
    ISofa createSofa();
    ICoffeeTable createCoffeeTable();
}

public class SphericFurnitureFactory implements IFurnitureFactory {
    public IChair createChair() {
        return new SphericChair();
    }

    public ISofa createSofa() {
        return new SphericSofa();
    }

    public ICoffeeTable createCoffeeTable() {
        return new SphericCoffeeTable();
    }
}

public class PyramidalFurnitureFactory implements IFurnitureFactory {
    public IChair createChair() {
        return new PyramidalChair();
    }

    public ISofa createSofa() {
        return new PyramidalSofa();
    }

    public ICoffeeTable createCoffeeTable() {
        return new PyramidalCoffeeTable();
    }
}

public class SphericChair implements IChair {
    public void sitOn() {
        System.out.println("Sit on a Spheric chair");
    }
}

public class PyramidalChair implements IChair {
    public void sitOn() {
        System.out.println("Sit on a Pyramidal chair");
    }
}

public class SphericSofa implements ISofa {
    public void sitOn() {
        System.out.println("Sit on a Spheric sofa");
    }
}

public class PyramidalSofa implements ISofa {
    public void sitOn() {
        System.out.println("Sit on a Pyramidal sofa");
    }
}

public class SphericCoffeeTable implements ICoffeeTable {
    public void putOn() {
        System.out.println("Put something on a Spheric coffee table");
    }
}

public class PyramidalCoffeeTable implements ICoffeeTable {
    public void putOn() {
        System.out.println("Put something on a Pyramidal coffee table");
    }
}

public class Main {
    public static void main(String[] args) {
        IFurnitureFactory factory = new SphericFurnitureFactory();

        IChair chair = factory.createChair();
        chair.sitOn();

        ISofa sofa = factory.createSofa();
        sofa.sitOn();

        ICoffeeTable coffeeTable = factory.createCoffeeTable();
        coffeeTable.putOn();

        factory = new PyramidalFurnitureFactory();

        chair = factory.createChair();
        chair.sitOn();

        sofa = factory.createSofa();
        sofa.sitOn();

        coffeeTable = factory.createCoffeeTable();
        coffeeTable.putOn();
    }
}


```

>     Ví dụ trên minh họa cách sử dụng mẫu thiết kế Abstract Factory để tạo ra các đối tượng nội thất liên quan mà không cần chỉ định các lớp cụ thể của chúng. Trong ví dụ này, chúng ta có hai loại nội thất: `Spheric` và `Pyramidal`, mỗi loại có các đối tượng `Chair`, `Sofa` và `CoffeeTable` riêng.
> 
>     Đầu tiên, chúng ta định nghĩa các giao diện cho mỗi loại đối tượng nội thất (`IChair`, `ISofa`, `ICoffeeTable`) và một giao diện `IFurnitureFactory` để tạo ra các đối tượng nội thất. Sau đó, chúng ta tạo ra các lớp cụ thể cho mỗi loại nội thất (`SphericChair`, `PyramidalChair`, …) và các lớp cụ thể cho `IFurnitureFactory` (`SphericFurnitureFactory`, `PyramidalFurnitureFactory`) để tạo ra các đối tượng nội thất cụ thể.
> 
>     Trong hàm `Main`, chúng ta tạo ra một đối tượng `IFurnitureFactory` và sử dụng nó để tạo ra các đối tượng nội thất. Sau đó chúng ta thay đổi loại nhà máy và tạo ra một bộ nội thất khác. Điều này cho phép chúng ta tạo ra các đối tượng nội thất phù hợp với nhau mà không cần chỉ định các lớp cụ thể của chúng.





`?`  **Trường hợp ta không dùng Abstract Factory thì sẽ như thế nào** 

    Nếu chúng ta không sử dụng mẫu thiết kế Abstract Factory trong ví dụ trên, chúng ta có thể tạo ra các đối tượng nội thất trực tiếp bằng cách sử dụng toán tử `new`. Tuy nhiên, điều này sẽ khiến mã của chúng ta trở nên cứng nhắc và khó bảo trì hơn.

```csharp
class Program
{
    static void Main(string[] args)
    {
        IChair chair = new SphericChair();
        chair.SitOn();

        ISofa sofa = new SphericSofa();
        sofa.SitOn();

        ICoffeeTable coffeeTable = new SphericCoffeeTable();
        coffeeTable.PutOn();

        chair = new PyramidalChair();
        chair.SitOn();

        sofa = new PyramidalSofa();
        sofa.SitOn();

        coffeeTable = new PyramidalCoffeeTable();
        coffeeTable.PutOn();
    }
}

```

>     Trong ví dụ này, chúng ta tạo ra các đối tượng nội thất bằng cách gọi trực tiếp các lớp cụ thể (`SphericChair`, `PyramidalSofa`, …). Điều này có thể dẫn đến các vấn đề sau:
> 
> * Nếu chúng ta muốn thay đổi loại nội thất được sử dụng (ví dụ: từ `Spheric` sang `Pyramidal`), chúng ta phải thay đổi mã ở nhiều nơi.
> * Nếu chúng ta muốn thêm một loại nội thất mới (ví dụ: `ArtDeco`), chúng ta phải thêm nhiều mã mới để xử lý loại nội thất mới này.
> * Việc kiểm tra mã trở nên khó khăn hơn vì chúng ta không thể dễ dàng thay thế các đối tượng nội thất bằng các đối tượng giả lập (mock objects).
> 
> Sử dụng mẫu thiết kế Abstract Factory giúp giải quyết các vấn đề trên bằng cách tách biệt việc tạo ra các đối tượng nội thất khỏi mã sử dụng chúng. Điều này cho phép chúng ta thay đổi loại nội thất được sử dụng một cách linh hoạt hơn và dễ dàng thêm các loại nội thất mới mà không cần thay đổi nhiều mã.



#### Vậy tới đây bạn sẽ thắc mắc

<mark>**Sự khác nhau giữa Abstract Factory và Factory Method là gì ?**</mark>

    Abstract Factory và Factory Method đều là các mẫu thiết kế khởi tạo (creational design patterns) giúp tách biệt việc tạo ra các đối tượng khỏi mã sử dụng chúng. Tuy nhiên, chúng có một số khác biệt quan trọng:

* **Abstract Factory** 
  
  > Được sử dụng để tạo ra các gia đình của các đối tượng liên quan mà không cần chỉ định các lớp cụ thể của chúng. Nó cung cấp một giao diện cho việc tạo ra các đối tượng thuộc các lớp khác nhau nhưng có liên quan với nhau. Ví dụ, một `IFurnitureFactory` có thể tạo ra các đối tượng `IChair`, `ISofa` và `ICoffeeTable` thuộc cùng một phong cách nội thất.

* **Factory Method** 
  
  > Được sử dụng để tạo ra một đối tượng của một lớp cụ thể, nhưng cho phép các lớp con quyết định lớp cụ thể nào sẽ được khởi tạo. Nó cung cấp một giao diện cho việc tạo ra một đối tượng của một lớp cụ thể, nhưng cho phép các lớp con ghi đè phương thức nhà máy để thay đổi loại đối tượng được tạo ra.

Về cơ bản, Abstract Factory là một bộ sưu tập các phương thức nhà máy (factory methods) để tạo ra các đối tượng liên quan với nhau. Trong khi Factory Method chỉ cung cấp một phương thức nhà máy duy nhất để tạo ra một đối tượng của một lớp cụ thể.
