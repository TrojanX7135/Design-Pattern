# Strategy Pattern

>    **Strategy Pattern** là một mẫu thiết kế thuộc nhóm hành vi (Behavioral Pattern).

---

<img title="Strategy pattern (mẫu chiến lược) là một mẫu thiết kế giúp bạn trừu tượng hóa những hành vi (behavior, method, function) của một đối tượng bằng cách đưa ra những cài đặt vào những lớp khác nhau. Mục đích của nó là định nghĩa và bao bọc các thuật toán có cùng mục đích trong những lớp có giao diện chung. Làm cho sự thay đổi thuật toán trở nên linh động và độc lập với khách hàng." src="https://refactoring.guru/images/patterns/content/strategy/strategy.png" alt="" data-align="center" style="zoom:100%;">

   Một ví dụ thực tế về việc áp dụng Strategy Pattern có thể là trong thiết kế ô tô. Bạn có thể tạo ra một lớp cơ sở có tên là Vehicle với một phương thức có tên là go. Sau đó, bạn tạo tiếp một lớp mới là lớp StreetRacer thừa kế từ lớp Vehicle. Tới đây, chương trình của bạn vẫn hoàn toàn tốt đẹp. Nhưng sau đó, bạn nhận thêm một hợp đồng sản xuất máy bay trực thăng Helicopter. Bạn nhận thấy máy bay trực thăng cũng là một phương tiện vận chuyển. Vì vậy bạn quyết định tạo ra một lớp Helicopter thừa kế từ lớp Vehicle. Nhưng khi sử dụng hàm go cho Helicopter, kết quả trả về không chính xác. Máy bay lại là driving? Máy bay thì phải bay chứ nhỉ? Đây là khi bạn có thể áp dụng Strategy Pattern để giải quyết vấn đề này.

#### # Khái niệm :

>     **Strategy Pattern** định nghĩa một tập hợp các thuật toán giống nhau, encapsulate chúng và khiến chúng có thể thay thế cho nhau. Strategy làm cho phần thuật toán độc lập khỏi client sử dụng nó.

 

#### # Sơ đồ UML Strategy Pattern :

<img title="UML Strategy pattern" src="https://www.dofactory.com/img/diagrams/net/strategy.png" alt="" data-align="center">

#### # Các thành phần :

Các lớp và đối tượng tham gia trong mẫu thiết kế này bao gồm:

* **Strategy (SortStrategy) :**
  
  * Khai báo một giao diện chung cho tất cả các thuật toán được hỗ trợ. Context sử dụng giao diện này để gọi thuật toán được định nghĩa bởi ConcreteStrategy.

* **ConcreteStrategy (QuickSort, ShellSort, MergeSort) :**
  
  * Triển khai thuật toán sử dụng giao diện Strategy.

* **Context (SortedList) :**
  
  * Được cấu hình với một đối tượng ConcreteStrategy.
  * Duy trì một tham chiếu đến một đối tượng Strategy.
  * Có thể định nghĩa một giao diện cho phép Strategy truy cập dữ liệu của nó.

#### # Ta hãy đến với ví dụ :

- **Structural code in C#**

   Đoạn Code cấu trúc này mô tả mẫu thiết kế Strategy, trong đó chức năng được đóng gói dưới dạng một đối tượng. Điều này cho phép khách hàng thay đổi động các chiến lược thuật toán.

```csharp

using System;

namespace Strategy.Structural
{
    /// <summary>
    /// Strategy Design Pattern
    /// </summary>

    public class Program
    {
        public static void Main(string[] args)
        {
            Context context;

            // Three contexts following different strategies

            context = new Context(new ConcreteStrategyA());
            context.ContextInterface();

            context = new Context(new ConcreteStrategyB());
            context.ContextInterface();

            context = new Context(new ConcreteStrategyC());
            context.ContextInterface();

            // Wait for user

            Console.ReadKey();
        }
    }

    /// <summary>
    /// The 'Strategy' abstract class
    /// </summary>

    public abstract class Strategy
    {
        public abstract void AlgorithmInterface();
    }

    /// <summary>
    /// A 'ConcreteStrategy' class
    /// </summary>

    public class ConcreteStrategyA : Strategy
    {
        public override void AlgorithmInterface()
        {
            Console.WriteLine(
                "Called ConcreteStrategyA.AlgorithmInterface()");
        }
    }

    /// <summary>
    /// A 'ConcreteStrategy' class
    /// </summary>

    public class ConcreteStrategyB : Strategy
    {
        public override void AlgorithmInterface()
        {
            Console.WriteLine(
                "Called ConcreteStrategyB.AlgorithmInterface()");
        }
    }

    /// <summary>
    /// A 'ConcreteStrategy' class
    /// </summary>

    public class ConcreteStrategyC : Strategy
    {
        public override void AlgorithmInterface()
        {
            Console.WriteLine(
                "Called ConcreteStrategyC.AlgorithmInterface()");
        }
    }

    /// <summary>
    /// The 'Context' class
    /// </summary>

    public class Context
    {
        Strategy strategy;

        // Constructor

        public Context(Strategy strategy)
        {
            this.strategy = strategy;
        }

        public void ContextInterface()
        {
            strategy.AlgorithmInterface();
        }
    }
}


```

**Output**

```powershell
Called ConcreteStrategyA.AlgorithmInterface()
Called ConcreteStrategyB.AlgorithmInterface()
Called ConcreteStrategyC.AlgorithmInterface()void ContextInterface()
```

>      Trong đó, `Strategy` là một lớp trừu tượng định nghĩa một phương thức `AlgorithmInterface()` để các lớp con cài đặt. Các lớp `ConcreteStrategyA`, `ConcreteStrategyB` và `ConcreteStrategyC` kế thừa từ lớp `Strategy` và cài đặt phương thức `AlgorithmInterface()` theo cách riêng của chúng.
> 
>     Lớp `Context` chứa một tham chiếu đến một đối tượng thuộc lớp `Strategy`. Nó có một phương thức `ContextInterface()` gọi phương thức `AlgorithmInterface()` của đối tượng thuộc lớp `Strategy`. Điều này cho phép chọn thuật toán được sử dụng tại thời điểm chạy bằng cách truyền vào một đối tượng thuộc lớp `ConcreteStrategyA`, `ConcreteStrategyB` hoặc `ConcreteStrategyC` cho hàm tạo của lớp `Context`.
> 
>     Trong hàm Main, ta tạo ra ba đối tượng thuộc lớp `Context` với ba chiến lược khác nhau và gọi phương thức `ContextInterface()` của chúng. Kết quả là các phương thức `AlgorithmInterface()` của các đối tượng thuộc lớp `ConcreteStrategyA`, `ConcreteStrategyB` và `ConcreteStrategyC` được gọi.



- **Real-world code in C#**

   Đoạn Code thực tế này mô tả mẫu thiết kế Strategy, trong đó thuật toán sắp xếp được đóng gói thành các đối tượng sắp xếp. Điều này cho phép khách hàng thay đổi động các chiến lược sắp xếp bao gồm Quicksort, Shellsort và Mergesort.

```csharp
using System;
using System.Collections.Generic;

namespace Strategy.RealWorld
{
    /// <summary>
    /// Strategy Design Pattern
    /// </summary>

    public class Program
    {
        public static void Main(string[] args)
        {
            // Two contexts following different strategies

            SortedList studentRecords = new SortedList();

            studentRecords.Add("Samual");
            studentRecords.Add("Jimmy");
            studentRecords.Add("Sandra");
            studentRecords.Add("Vivek");
            studentRecords.Add("Anna");

            studentRecords.SetSortStrategy(new QuickSort());
            studentRecords.Sort();

            studentRecords.SetSortStrategy(new ShellSort());
            studentRecords.Sort();

            studentRecords.SetSortStrategy(new MergeSort());
            studentRecords.Sort();

            // Wait for user

            Console.ReadKey();
        }
    }

    /// <summary>
    /// The 'Strategy' abstract class
    /// </summary>

    public abstract class SortStrategy
    {
        public abstract void Sort(List<string> list);
    }

    /// <summary>
    /// A 'ConcreteStrategy' class
    /// </summary>

    public class QuickSort : SortStrategy
    {
        public override void Sort(List<string> list)
        {
            list.Sort();  // Default is Quicksort
            Console.WriteLine("QuickSorted list ");
        }
    }

    /// <summary>
    /// A 'ConcreteStrategy' class
    /// </summary>

    public class ShellSort : SortStrategy
    {
        public override void Sort(List<string> list)
        {
            //list.ShellSort();  not-implemented
            Console.WriteLine("ShellSorted list ");
        }
    }

    /// <summary>
    /// A 'ConcreteStrategy' class
    /// </summary>

    public class MergeSort : SortStrategy
    {
        public override void Sort(List<string> list)
        {
            //list.MergeSort(); not-implemented

            Console.WriteLine("MergeSorted list ");
        }
    }

    /// <summary>
    /// The 'Context' class
    /// </summary>

    public class SortedList
    {
        private List<string> list = new List<string>();
        private SortStrategy sortstrategy;

        public void SetSortStrategy(SortStrategy sortstrategy)
        {
            this.sortstrategy = sortstrategy;
        }

        public void Add(string name)
        {
            list.Add(name);
        }

        public void Sort()
        {
            sortstrategy.Sort(list);

            // Iterate over list and display results

            foreach (string name in list)
            {
                Console.WriteLine(" " + name);
            }
            Console.WriteLine();
        }
    }
}


```

**Output**

```powershell
QuickSorted list
 Anna
 Jimmy
 Samual
 Sandra
 Vivek

ShellSorted list
 Anna
 Jimmy
 Samual
 Sandra
 Vivek

MergeSorted list
 Anna
 Jimmy
 Samual
 Sandra
 Vivek
```

>     Trong đó, `SortStrategy` là một lớp trừu tượng định nghĩa một phương thức `Sort()` để các lớp con cài đặt. Các lớp `QuickSort`, `ShellSort` và `MergeSort` kế thừa từ lớp `SortStrategy` và cài đặt phương thức `Sort()` theo cách riêng của chúng.
> 
>     Lớp `SortedList` chứa một danh sách các chuỗi và một tham chiếu đến một đối tượng thuộc lớp `SortStrategy`. Nó có một phương thức `SetSortStrategy()` để thiết lập chiến lược sắp xếp và một phương thức `Sort()` gọi phương thức `Sort()` của đối tượng thuộc lớp `SortStrategy`. Điều này cho phép chọn thuật toán sắp xếp được sử dụng tại thời điểm chạy bằng cách truyền vào một đối tượng thuộc lớp `QuickSort`, `ShellSort` hoặc `MergeSort` cho phương thức `SetSortStrategy()`.
> 
>     Trong hàm Main, ta tạo ra một đối tượng thuộc lớp `SortedList`, thêm một số phần tử vào danh sách và sắp xếp danh sách theo ba chiến lược khác nhau. Kết quả là các phương thức `Sort()` của các đối tượng thuộc lớp `QuickSort`, `ShellSort` và `MergeSort` được gọi.


