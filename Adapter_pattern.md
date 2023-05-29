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

- **Structural code in C#**

    Đoạn mã này mô tả mẫu thiết kế Adapter, giúp ánh xạ giao diện của một lớp vào một lớp khác để chúng có thể hoạt động cùng nhau. Các lớp không tương thích này có thể đến từ các thư viện hoặc khung công việc khác nhau.

```csharp

using System;

namespace Adapter.Structural
{
    public class Program
    {
        public static void Main(string[] args)
        {
            // Khởi tạo một đối tượng Adapter và gọi phương thức Request()
            Target target = new Adapter();
            target.Request();

            Console.ReadKey();
        }
    }

    // Class Target định nghĩa interface mà client sử dụng
    public class Target
    {
        public virtual void Request()
        {
            Console.WriteLine("Called Target Request()"); // yêu cầu mà Target gọi
        }
    }

    // Class Adapter kế thừa từ class Target và chứa một đối tượng Adaptee
    public class Adapter : Target
    {
        private Adaptee adaptee = new Adaptee();

        public override void Request()
        {
            // gọi phương thức SpecificRequest()
            adaptee.SpecificRequest();
        }
    }

    // Class Adaptee chứa một phương thức SpecificRequest()
    public class Adaptee
    {
        public void SpecificRequest()
        {
            Console.WriteLine("Called SpecificRequest()"); // yêu cầu cụ thể nằm bên adaptee
        }
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



- **Real-world code in C#**

   Đoạn mã thực tế này mô tả việc sử dụng một cơ sở dữ liệu hóa chất cũ. Các đối tượng hợp chất hóa học truy cập cơ sở dữ liệu thông qua một giao diện Adapter.

```csharp
using System;

namespace Adapter.RealWorld
{
    public class Program
    {
        public static void Main(string[] args)
        {
            // Hợp chất không được điều chỉnh
            Compound unknown = new Compound();
            unknown.Display();

            // Hợp chất được điều chỉnh
            Compound water = new RichCompound("Water");
            water.Display();

            Compound benzene = new RichCompound("Benzene");
            benzene.Display();

            Compound ethanol = new RichCompound("Ethanol");
            ethanol.Display();

            // Chờ người dùng
            Console.ReadKey();
        }
    }

    /// Lớp 'Target'
    public class Compound
    {
        protected float boilingPoint;
        protected float meltingPoint;
        protected double molecularWeight;
        protected string molecularFormula;

        public virtual void Display()
        {
            Console.WriteLine("\nHợp chất: Không xác định ------ ");
        }
    }

    /// Lớp 'Adapter'
    public class RichCompound : Compound
    {
        private string chemical;
        private ChemicalDatabank bank;

        // Constructor
        public RichCompound(string chemical)
        {
            this.chemical = chemical;
        }

        public override void Display()
        {
            // Adaptee
            bank = new ChemicalDatabank();
            boilingPoint = bank.GetCriticalPoint(chemical, "B");
            meltingPoint = bank.GetCriticalPoint(chemical, "M");
            molecularWeight = bank.GetMolecularWeight(chemical);
            molecularFormula = bank.GetMolecularStructure(chemical);

            Console.WriteLine("\nHợp chất: {0} ------ ", chemical);
            Console.WriteLine(" Công thức: {0}", molecularFormula);
            Console.WriteLine(" Khối lượng: {0}", molecularWeight);
            Console.WriteLine(" Điểm nóng chảy: {0}", meltingPoint);
            Console.WriteLine(" Điểm sôi: {0}", boilingPoint);
        }
    }

    /// Lớp 'Adaptee'
    public class ChemicalDatabank
    {
        public float GetCriticalPoint(string compound, string point)
        {
            // Điểm nóng chảy
            if (point == "M")
            {
                switch (compound.ToLower())
                {
                    case "water": return 0.0f;
                    case "benzene": return 5.5f;
                    case "ethanol": return -114.1f;
                    default: return 0f;
                }
            }
            // Điểm sôi
            else
            {
                switch (compound.ToLower())
                {
                    case "water": return 100.0f;
                    case "benzene": return 80.1f;
                    case "ethanol": return 78.3f;
                    default: return 0f;
                }
            }
        }

        public string GetMolecularStructure(string compound)
        {
            switch (compound.ToLower())
            {
                case "water": return "H20";
                case "benzene": return "C6H6";
                case "ethanol": return "C2H5OH";
                default: return "";
            }
        }

        public double GetMolecularWeight(string compound)
        {
            switch (compound.ToLower())
            {
                case "water": return 18.015;
                case "benzene": return 78.1134;
                case "ethanol": return 46.0688;
                default: return 0d;
            }
        }
    }
}



```

**Output**

```powershell
Hợp chất: Không xác định ------

Hợp chất: Water ------
Công thức: H20
Khối lượng: 18.015
Điểm nóng chảy: 0
Điểm sôi: 100

Hợp chất: Benzene ------
Công thức: C6H6
Khối lượng: 78.1134
Điểm nóng chảy: 5.5
Điểm sôi: 80.1

Hợp chất: Ethanol ------
Công thức: C2H5OH
Khối lượng: 46.0688
Điểm nóng chảy: -114.1
Điểm sôi: 78.3
```

>     Trong đó:
> 
> - Lớp `Compound` là lớp mục tiêu (Target) trong mẫu thiết kế. Nó định nghĩa phương thức `Display()` để hiển thị thông tin về hợp chất. Đây là giao diện mà lớp `RichCompound` sẽ sử dụng để tương tác với hệ thống.
> 
> - Lớp `RichCompound` là lớp Adapter. Nó kế thừa từ lớp `Compound` và cung cấp một giao diện tương thích với hệ thống hiện tại. Lớp này chứa một đối tượng của lớp `ChemicalDatabank` và gọi các phương thức của nó để lấy thông tin về hợp chất.
> 
> - Lớp `ChemicalDatabank` là lớp Adaptee, đại diện cho hệ thống hiện tại. Nó cung cấp các phương thức để truy xuất thông tin về các hợp chất từ một nguồn dữ liệu.
> 
> - Trong phương thức `Display()` của lớp `RichCompound`, lớp này sử dụng đối tượng `ChemicalDatabank` để lấy thông tin về hợp chất (như boiling point, melting point, molecular weight, molecular formula) thông qua các phương thức của nó.
> 
> Với cách triển khai này, lớp `RichCompound` cung cấp một giao diện tương thích với lớp `Compound` (lớp mục tiêu), nhưng nó sử dụng lớp `ChemicalDatabank` (lớp Adaptee) để lấy thông tin về hợp chất từ hệ thống hiện tại. Điều này cho phép lớp `Compound` tương tác với hệ thống thông qua lớp `RichCompound` như là một Adapter.


