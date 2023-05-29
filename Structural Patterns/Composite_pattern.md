# Composite Pattern

>     **Composite Pattern**  là một design pattern thuộc nhóm cấu trúc ( Structure Design Pattern ).
> 
>     Composite Pattern thuộc nhóm structural pattern vì nó tạo ra cấu trúc phân cấp và hợp thành giữa các đối tượng để tạo thành một đối tượng lớn hơn. Pattern này cho phép đối tượng cá nhân và các đối tượng tổng hợp được xem như nhau thông qua việc triển khai chung một interface hoặc lớp cơ sở.

---

<img title="Composite Pattern tổ chức các đối tượng theo cấu trúc cây để diễn giải một phần hoặc toàn bộ hệ thống phân cấp" src="https://refactoring.guru/images/patterns/content/composite/composite.png?id=73bcf0d94db360b636cd745f710d19db" alt="" data-align="center" style="zoom:100%;">

#### # Khái niệm :

>     **Composite Pattern** là một mẫu thiết kế thuộc nhóm cấu trúc (Structural Pattern). 
> 
>     Composite Pattern là một sự tổng hợp những thành phần có quan hệ với nhau để tạo ra thành phần lớn hơn. Nó cho phép thực hiện các tương tác với tất cả đối tượng trong mẫu tương tự nhau.

    

    Composite Pattern được sử dụng khi chúng ta cần xử lý một nhóm đối tượng tương tự theo cách xử lý một đối tượng đơn lẻ. Pattern Composite tổ chức các đối tượng theo cấu trúc cây để diễn giải một phần hoặc toàn bộ hệ thống phân cấp. Pattern này tạo ra một lớp chứa nhóm đối tượng của riêng nó. Lớp này cung cấp các phương thức để thay đổi nhóm của một đối tượng duy nhất. Pattern này cho phép Client viết mã giống nhau để tương tác với đối tượng Composite này, bất kể đó là một đối tượng đơn lẻ hay tập hợp các đối tượng. 

    Ví dụ: bạn có hai loại đối tượng: Sản phẩm và Hộp. Một Hộp có thể chứa nhiều Sản phẩm cũng như một số Hộp nhỏ hơn. Những chiếc Hộp nhỏ này có thể cũng giữ một số Sản phẩm hoặc thậm chí các Hộp nhỏ hơn, v.v.

<img title="Làm thế nào bạn sẽ xác định tổng giá của một đơn đặt hàng như vậy?" src="https://images.viblo.asia/79ef6968-27a6-49c7-a6cb-78bcd37e5804.png" alt="" data-align="center" style="zoom:80%;">

    Giả sử bạn quyết định tạo một hệ thống đặt hàng. Làm thế nào bạn sẽ xác định tổng giá của một đơn đặt hàng như vậy ? 

    Bạn có thể mở tất cả các hộp, xem qua tất cả các sản phẩm và sau đó tính tổng. Nhưng cách tiếp cận này khi thực thi chương trình đòi hỏi mức độ lồng ghép và cấu trúc phức tạp.

    Giải pháp: Composite pattern cho phép làm việc với Sản phẩm và Hộp thông qua một giao diện chung khai báo một phương pháp tính tổng giá. Đối với một hộp, nó sẽ đi qua từng mục trong hộp chứa, hỏi giá của nó và sau đó trả lại tổng giá cho hộp này. Lợi ích lớn nhất của phương pháp này là không cần phải quan tâm đến các lớp cụ thể của các đối tượng tạo ra và xử lý chúng với cùng một phương thức.

<img title="Composite pattern work" src="https://images.viblo.asia/33426952-6848-43d6-9b07-88d9ee9436d7.png" alt="" style="zoom:67%;" data-align="center">

#### # Sơ đồ UML Composite Pattern :

<img title="UML Composite pattern" src="https://www.dofactory.com/img/diagrams/net/composite.png" alt="" data-align="center">

#### 

#### # Các thành phần:

- **Component (DrawingElement) :** *Định nghĩa giao diện hoặc lớp cơ sở cho các đối tượng trong cấu trúc phân cấp.*
  
  - Component định nghĩa giao diện chung cho cả leaf và composite.
  
  - Component khai báo các phương thức chung mà cả hai loại đối tượng leaf và composite phải triển khai, chẳng hạn như phương thức thêm, xoá và hiển thị thành phần.
  
  - Component cung cấp một giao diện thống nhất cho cả leaf và composite, cho phép chúng được sử dụng thay thế nhau.
    
    

- **Leaf (PrimitiveElement) :** Node Lá - *Đại diện cho các đối tượng cá nhân trong cấu trúc phân cấp, không có con.*
  
  - Leaf là thành phần cơ bản, không có các thành phần con bên trong.
  
  - Leaf triển khai các phương thức của Component và thực hiện chúng theo cách tương ứng với các yêu cầu của đối tượng lá.
  
  - Leaf không thể chứa các thành phần con, vì nó là đơn giản và không thể phân chia thành các thành phần nhỏ hơn.
    
    
* **Composite (CompositeElement) :** Node - *Đại diện cho các đối tượng tổng hợp trong cấu trúc phân cấp, có thể chứa các đối tượng con bao gồm cả các đối tượng leaf node và composite node khác.*
  
  * Composite là thành phần phức tạp hơn, có thể chứa các thành phần con khác (bao gồm cả leaf và composite).
  
  * Composite triển khai các phương thức của Component để thêm, xoá và hiển thị thành phần.
  
  * Composite cũng duy trì một danh sách các thành phần con và gọi các phương thức tương ứng của chúng khi được yêu cầu.
    
    

* **Client (CompositeApp) :**
  
  * Tương tác với các đối tượng trong cấu trúc tổng hợp thông qua giao diện Component.
    
    

#### # Ta hãy đến với ví dụ :

- **Structural code in C#**

    Đoạn Code cấu trúc này mô tả mẫu thiết kế Composite, cho phép tạo ra một cấu trúc cây trong đó các nút cá nhân được truy cập theo cách đồng nhất, cho dù chúng là nút lá hoặc nút nhánh (composite).

```csharp

using System;
using System.Collections.Generic;

namespace Composite.Structural
{

    public class Program
    {
        public static void Main(string[] args)
        {
            // Create a tree structure

            Composite root = new Composite("root");
            root.Add(new Leaf("Leaf A"));
            root.Add(new Leaf("Leaf B"));

            Composite comp = new Composite("Composite X");
            comp.Add(new Leaf("Leaf XA"));
            comp.Add(new Leaf("Leaf XB"));

            root.Add(comp);
            root.Add(new Leaf("Leaf C"));

            // Add and remove a leaf

            Leaf leaf = new Leaf("Leaf D");
            root.Add(leaf);
            root.Remove(leaf);

            // Recursively display tree

            root.Display(1);

            Console.ReadKey();
        }
    }

    public abstract class Component
    {
        protected string name;

        // Constructor

        public Component(string name)
        {
            this.name = name;
        }

        public abstract void Add(Component c);
        public abstract void Remove(Component c);
        public abstract void Display(int depth);
    }

    public class Composite : Component
    {
        List<Component> children = new List<Component>();

        // Constructor

        public Composite(string name)
            : base(name)
        {
        }

        public override void Add(Component component)
        {
            children.Add(component);
        }

        public override void Remove(Component component)
        {
            children.Remove(component);
        }

        public override void Display(int depth)
        {
            Console.WriteLine(new String('-', depth) + name);

            // Recursively display child nodes

            foreach (Component component in children)
            {
                component.Display(depth + 2);
            }
        }
    }

    public class Leaf : Component
    {
        // Constructor

        public Leaf(string name)
            : base(name)
        {
        }

        public override void Add(Component c)
        {
            Console.WriteLine("Cannot add to a leaf");
        }

        public override void Remove(Component c)
        {
            Console.WriteLine("Cannot remove from a leaf");
        }

        public override void Display(int depth)
        {
            Console.WriteLine(new String('-', depth) + name);
        }
    }
}





```

**Output**

```powershell
-root
---Leaf A
---Leaf B
---Composite X
-----Leaf XA
-----Leaf XB
---Leaf C
```

>    Trong đó, chúng ta có các lớp sau:
> 
> * `Component`: là một lớp trừu tượng định nghĩa các phương thức chung cho tất cả các thành phần trong cây. Trong ví dụ này, các phương thức bao gồm `Add`, `Remove` và `Display`.
> * `Composite`: là một lớp kế thừa từ `Component` và đại diện cho các đối tượng tổng hợp có con cái. Lớp này chứa một danh sách các đối tượng con và cài đặt các phương thức của `Component` bằng cách ủy nhiệm cho các đối tượng con xử lý.
> * `Leaf`: là một lớp kế thừa từ `Component` và đại diện cho các đối tượng lá không có con cái. Lớp này cài đặt các phương thức của `Component` một cách trực tiếp.
> 
> Trong hàm `Main`, chúng ta tạo ra một cây bằng cách khởi tạo một đối tượng gốc kiểu `Composite` và thêm vào nó các đối tượng lá và tổng hợp khác. Sau đó, chúng ta gọi phương thức `Display` của đối tượng gốc để hiển thị toàn bộ cây theo cấu trúc phân cấp.
> 
> `List<Component>` là một lớp trong thư viện `System.Collections.Generic` của .NET Framework. Nó đại diện cho một danh sách các đối tượng có thể truy cập theo chỉ mục và cung cấp các phương thức để thêm, xóa và tìm kiếm các phần tử trong danh sách.
> 
> Trong đoạn code mẫu này, lớp `Composite` sử dụng một đối tượng `List<Component>` để lưu trữ danh sách các đối tượng con kiểu `Component`. Các phương thức `Add` và `Remove` của lớp `Composite` được cài đặt bằng cách gọi các phương thức tương ứng của lớp `List<Component>` để thêm hoặc xóa các đối tượng con.



- **Real-world code in C#**

   Đoạn Code thực tế này mô tả mẫu thiết kế Composite được sử dụng để xây dựng một cấu trúc cây đồ họa gồm các nút nguyên thủy (đường, hình tròn, v.v.) và các nút composite (nhóm các thành phần vẽ tạo thành các yếu tố phức tạp hơn).

```csharp
using System;
using System.Collections.Generic;

namespace Composite.RealWorld
{
    /// Composite Design Pattern

    public class Program
    {
        public static void Main(string[] args)
        {
            // Create a tree structure 

            CompositeElement root = new CompositeElement("Picture");
            root.Add(new PrimitiveElement("Red Line"));
            root.Add(new PrimitiveElement("Blue Circle"));
            root.Add(new PrimitiveElement("Green Box"));

            // Create a branch

            CompositeElement comp = new CompositeElement("Two Circles");
            comp.Add(new PrimitiveElement("Black Circle"));
            comp.Add(new PrimitiveElement("White Circle"));
            root.Add(comp);

            /*
            CompositeElement comp1 = new CompositeElement("Two Triangle");
            comp1.Add(new PrimitiveElement("Black white Triangle"));
            comp1.Add(new PrimitiveElement("White black Triangle"));
            comp.Add(comp1);*/

            // Add and remove a PrimitiveElement

            PrimitiveElement pe = new PrimitiveElement("Yellow Line");
            root.Add(pe);
            root.Remove(pe);

            // Recursively display nodes

            root.Display(1);

            Console.ReadKey();
        }
    }

    /// The 'Component' Treenode
    public abstract class DrawingElement
    {
        protected string name;

        public DrawingElement(string name)
        {
            this.name = name;
        }

        public abstract void Add(DrawingElement d);
        public abstract void Remove(DrawingElement d);
        public abstract void Display(int indent);
    }

    /// The 'Leaf' class
    public class PrimitiveElement : DrawingElement
    {
        public PrimitiveElement(string name)
            : base(name)
        {
        }

        public override void Add(DrawingElement c)
        {
            Console.WriteLine(
                "Cannot add to a PrimitiveElement");
        }

        public override void Remove(DrawingElement c)
        {
            Console.WriteLine(
                "Cannot remove from a PrimitiveElement");
        }

        public override void Display(int indent)
        {
            Console.WriteLine(
                new String('-', indent) + " " + name);
        }
    }

    /// The 'Composite' class
    public class CompositeElement : DrawingElement
    {
        List<DrawingElement> elements = new List<DrawingElement>();

        public CompositeElement(string name)
            : base(name)
        {
        }

        public override void Add(DrawingElement d)
        {
            elements.Add(d);
        }

        public override void Remove(DrawingElement d)
        {
            elements.Remove(d);
        }

        public override void Display(int indent)
        {
            Console.WriteLine(new String('-', indent) +
                "+ " + name);

            // Display each child element on this node

            foreach (DrawingElement d in elements)
            {
                d.Display(indent + 2);
            }
        }
    }
}


/*
Console.WriteLine("- Picture");
Console.WriteLine("-- Red Line");
Console.WriteLine("-- Blue Circle");
Console.WriteLine("-- Green Box");
Console.WriteLine("-- Two Circles");
Console.WriteLine("---- White Circle");
Console.WriteLine("---- Black Circle");
Console.WriteLine("------ Small Black Circle");
Console.WriteLine("------ Big Black Circle");
*/


```

**Output**

```powershell
-+ Picture
--- Red Line
--- Blue Circle
--- Green Box
---+ Two Circles
----- Black Circle
----- White Circle
```

>     Trong đó, chúng ta có các lớp sau:
> 
> * `DrawingElement`: là một lớp trừu tượng định nghĩa các phương thức chung cho tất cả các thành phần trong cây. Trong ví dụ này, các phương thức bao gồm `Add`, `Remove` và `Display`.
> * `CompositeElement`: là một lớp kế thừa từ `DrawingElement` và đại diện cho các đối tượng tổng hợp có con cái. Lớp này chứa một danh sách các đối tượng con và cài đặt các phương thức của `DrawingElement` bằng cách ủy nhiệm cho các đối tượng con xử lý.
> * `PrimitiveElement`: là một lớp kế thừa từ `DrawingElement` và đại diện cho các đối tượng lá không có con cái. Lớp này cài đặt các phương thức của `DrawingElement` một cách trực tiếp.
> 
> Trong hàm `Main`, chúng ta tạo ra một cây bằng cách khởi tạo một đối tượng gốc kiểu `CompositeElement` và thêm vào nó các đối tượng lá và tổng hợp khác. Sau đó, chúng ta gọi phương thức `Display` của đối tượng gốc để hiển thị toàn bộ cây theo cấu trúc phân cấp.
