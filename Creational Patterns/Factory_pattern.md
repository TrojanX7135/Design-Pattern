# Factory Pattern

>     **Factory Pattern**  là một design pattern thuộc nhóm khởi tạo (Creational patterns).

---

<img title="Factory Pattern" src="https://refactoring.guru/images/patterns/content/factory-method/factory-method-en.png?id=cfa26f33dc8473e803fadae0d262100a" alt="" data-align="center" style="zoom:100%;">

#### Khái niệm :

>     Pattern này được sinh ra nhằm mục đích khởi tạo một đối tượng mới mà không cần thiết phải chỉ ra một cách chính xác class nào sẽ được khởi tạo.
> 
>     **Factory Method Pattern** giải quyết vấn đề này bằng cách định nghĩa một factory method cho việc tạo đối tượng, và các lớp con thừa kế có thể override phương thức này để chỉ rõ đối tượng nào sẽ được khởi tạo.

#### Ta hãy đến với ví dụ :

    Một ví dụ về việc sử dụng Factory Pattern trong C#...  

```csharp

public interface IAnimal
{
    string Speak();
}

public class Dog : IAnimal
{
    public string Speak()
    {
        return "Gâu gâu";
    }
}

public class Cat : IAnimal
{
    public string Speak()
    {
        return "Meo meo";
    }
}

public abstract class AnimalFactory
{
    public abstract IAnimal GetAnimal(string animalType);
}

public class ConcreteAnimalFactory : AnimalFactory
{
    public override IAnimal GetAnimal(string animalType)
    {
        switch (animalType)
        {
            case "Dog":
                return new Dog();
            case "Cat":
                return new Cat();
            default:
                throw new Exception("Invalid animal type");
        }
    }
}

```

>     Trong ví dụ trên, chúng ta có một `AnimalFactory` để tạo ra các đối tượng `IAnimal` dựa trên tham số `animalType`. Điều này cho phép chúng ta tạo ra các đối tượng mà không cần biết lớp cụ thể của chúng.
> 
>     `AnimalFactory` là một lớp trừu tượng có một phương thức trừu tượng `GetAnimal()` nhận vào một tham số `animalType` và trả về một đối tượng `IAnimal`. Lớp kế thừa từ `AnimalFactory` sẽ cần phải thực hiện phương thức này để tạo ra các đối tượng `IAnimal` cụ thể.



    Nếu bạn muốn thêm vào đó một con gà ?
    Bạn có thể tạo một lớp `Chicken` kế thừa từ `IAnimal` và thực hiện phương thức `Speak()`

```csharp
public class Chicken : IAnimal
{
    public string Speak()
    {
        return "Ò ó o";
    }
}

```

    Sau đó, bạn có thể thêm một trường hợp cho `Chicken` trong phương thức `GetAnimal()` của lớp `ConcreteAnimalFactory`:

```csharp
public class ConcreteAnimalFactory : AnimalFactory
{
    public override IAnimal GetAnimal(string animalType)
    {
        switch (animalType)
        {
            case "Dog":
                return new Dog();
            case "Cat":
                return new Cat();
            case "Chicken":
                return new Chicken();
            default:
                throw new Exception("Invalid animal type");
        }
    }
}

```

    Với cách làm này, bạn có thể tạo ra một đối tượng `Chicken` bằng cách gọi phương thức `GetAnimal("Chicken")`.



`?` **Trường hợp ta không dùng Factory thì sẽ như thế nào**

    Dưới đây là ví dụ nếu không dùng factory pattern...

```csharp
public interface IAnimal
{
    string Speak();
}

public class Dog : IAnimal
{
    public string Speak()
    {
        return "Gâu gâu";
    }
}

public class Cat : IAnimal
{
    public string Speak()
    {
        return "Meo meo";
    }
}

class Program
{
    static void Main(string[] args)
    {
        IAnimal animal;
        string animalType = "Dog";

        if (animalType == "Dog")
        {
            animal = new Dog();
        }
        else if (animalType == "Cat")
        {
            animal = new Cat();
        }
        else
        {
            throw new Exception("Invalid animal type");
        }

        Console.WriteLine(animal.Speak());
    }
}


```

    Trong ví dụ trên, chúng ta tạo ra một đối tượng `IAnimal` bằng cách sử dụng từ khóa `new` và kiểm tra giá trị của biến `animalType` để xác định loại động vật cần tạo.

   Việc tạo ra các đối tượng một cách trực tiếp như vậy làm cho code của bạn trở nên phụ thuộc vào các lớp cụ thể, khiến cho việc thay đổi và bảo trì code trở nên khó khăn hơn.

>     *Factory pattern giúp giải quyết các vấn đề này bằng cách tạo ra một lớp factory để quản lý việc tạo ra các đối tượng. Điều này cho phép bạn tạo ra các đối tượng mà không cần biết lớp cụ thể của chúng và giúp cho code của bạn dễ thay đổi và bảo trì hơn.*
