# Iterator Pattern

>    **Iterator Pattern** là một mẫu thiết kế thuộc nhóm hành vi (Behavioral Pattern).

---

<img title="Người ra lệnh cần cung cấp một class đóng gói những mệnh lệnh. Người nhận mệnh lệnh cần phân biệt những interface nào để thực hiện đúng mệnh lệnh." src="https://refactoring.guru/images/patterns/content/iterator/iterator-en.png" alt="" data-align="center" style="zoom:100%;">

   Một ví dụ thực tế gần gũi về Iterator pattern có thể là khi bạn đang duyệt qua một danh sách bài hát trên một ứng dụng nghe nhạc. Bạn có thể sử dụng các nút “next” và “previous” để di chuyển qua lại giữa các bài hát mà không cần biết chi tiết về cách danh sách bài hát được lưu trữ và quản lý. Đây chính là Iterator pattern đang được áp dụng.

#### # Khái niệm :

>    **Iterator pattern** được thiết kế cho phép xử lý nhiều loại tập hợp khác nhau bằng cách truy cập những phần tử của tập hợp với cùng một phương pháp, cùng một cách thức định sẵn, mà không cần phải hiểu rõ về những chi tiết bên trong của những tập hợp này.
> 
>     Nói cách khác, một Iterator được thiết kế cho phép xử lý nhiều loại tập hợp khác nhau bằng cách truy cập những phần tử của tập hợp với cùng một phương pháp, cùng một cách thức định sẵn, mà không cần phải hiểu rõ về những chi tiết bên trong của những tập hợp này.
> 
>     Ý tưởng thiết kế này là một trong những kỹ thuật được gọi là “đơn trách nhiệm – Single responsibility principle (SRP)” – một lớp chỉ có duy nhất một công việc để làm. Hãy suy nghĩ rằng tập hợp duy trì các phần tử, một iterator cung cấp cách thức làm việc với các phần tử đó. Đó cũng là lý do tại sao những Iterator có thể làm việc được trong các tập hợp khác nhau.

 

#### # Sơ đồ UML Iterator Pattern :

<img title="UML Iterator pattern" src="https://www.dofactory.com/img/diagrams/net/iterator.png" alt="" data-align="center">

#### # Các thành phần :

Các lớp và đối tượng tham gia trong mẫu thiết kế này bao gồm:

* **Iterator (AbstractIterator) :**
  
  * Định nghĩa một giao diện để truy cập và duyệt qua các phần tử.

* **ConcreteIterator (Iterator) :**
  
  * Triển khai giao diện Iterator.
  * Theo dõi vị trí hiện tại trong quá trình duyệt qua tập hợp.

* **Aggregate (AbstractCollection) :**
  
  * Định nghĩa một giao diện để tạo ra một đối tượng Iterator.

* **ConcreteAggregate (Collection) :**
  
  * Triển khai giao diện tạo Iterator để trả về một thể hiện của ConcreteIterator thích hợp.
    
    

#### # Ta hãy đến với ví dụ :

- **Structural code in C#**

    Đoạn Code cấu trúc này mô tả mẫu thiết kế Iterator, cung cấp cách để duyệt (lặp) qua một tập hợp các phần tử mà không cần biết chi tiết về cấu trúc nội bộ của tập hợp đó.

```csharp

using System;
using System.Collections.Generic;

namespace Iterator.Structural
{
    /// <summary>
    /// Iterator Design Pattern
    /// </summary>

    public class Program
    {
        public static void Main(string[] args)
        {
            ConcreteAggregate a = new ConcreteAggregate();
            a[0] = "Item A";
            a[1] = "Item B";
            a[2] = "Item C";
            a[3] = "Item D";

            // Create Iterator and provide aggregate

            Iterator i = a.CreateIterator();

            Console.WriteLine("Iterating over collection:");

            object item = i.First();

            while (item != null)
            {
                Console.WriteLine(item);
                item = i.Next();
            }

            // Wait for user

            Console.ReadKey();
        }
    }

    /// <summary>
    /// The 'Aggregate' abstract class
    /// </summary>

    public abstract class Aggregate
    {
        public abstract Iterator CreateIterator();
    }

    /// <summary>
    /// The 'ConcreteAggregate' class
    /// </summary>

    public class ConcreteAggregate : Aggregate
    {
        List<object> items = new List<object>();

        public override Iterator CreateIterator()
        {
            return new ConcreteIterator(this);
        }

        // Get item count

        public int Count
        {
            get { return items.Count; }
        }

        // Indexer

        public object this[int index]
        {
            get { return items[index]; }
            set { items.Insert(index, value); }
        }
    }

    /// <summary>
    /// The 'Iterator' abstract class
    /// </summary>

    public abstract class Iterator
    {
        public abstract object First();
        public abstract object Next();
        public abstract bool IsDone();
        public abstract object CurrentItem();
    }

    /// <summary>
    /// The 'ConcreteIterator' class
    /// </summary>

    public class ConcreteIterator : Iterator
    {
        ConcreteAggregate aggregate;
        int current = 0;

        // Constructor

        public ConcreteIterator(ConcreteAggregate aggregate)
        {
            this.aggregate = aggregate;
        }

        // Gets first iteration item

        public override object First()
        {
            return aggregate[0];
        }

        // Gets next iteration item

        public override object Next()
        {
            object ret = null;
            if (current < aggregate.Count - 1)
            {
                ret = aggregate[++current];
            }

            return ret;
        }

        // Gets current iteration item

        public override object CurrentItem()
        {
            return aggregate[current];
        }

        // Gets whether iterations are complete

        public override bool IsDone()
        {
            return current >= aggregate.Count;
        }
    }
}


```

**Output**

```powershell
Iterating over collection:
Item A
Item B
Item C
Item D
```

>   Trong đó, `ConcreteAggregate` là một lớp cụ thể của `Aggregate` và chứa một danh sách các đối tượng. Lớp `ConcreteIterator` là một lớp cụ thể của `Iterator` và được sử dụng để duyệt qua các phần tử của `ConcreteAggregate`.
> 
>     Trong hàm `Main`, một đối tượng `ConcreteAggregate` được khởi tạo và các phần tử được thêm vào. Sau đó, một đối tượng `Iterator` được tạo ra bằng cách gọi phương thức `CreateIterator()` của đối tượng `ConcreteAggregate`. Cuối cùng, chương trình sử dụng đối tượng `Iterator` để duyệt qua các phần tử của `ConcreteAggregate` và in chúng ra màn hình.
> 
> Các phương thức của lớp `ConcreteIterator` bao gồm:
> 
> * `First()`: Trả về phần tử đầu tiên của danh sách.
> * `Next()`: Trả về phần tử tiếp theo trong danh sách.
> * `CurrentItem()`: Trả về phần tử hiện tại trong danh sách.
> * `IsDone()`: Kiểm tra xem đã duyệt hết danh sách chưa.



- **Real-world code in C#**

   Đoạn Code thực tế này mô tả mẫu thiết kế Iterator được sử dụng để duyệt qua một tập hợp các phần tử và bỏ qua một số phần tử cụ thể trong mỗi vòng lặp.

```csharp
using System;
using System.Collections.Generic;

namespace Iterator.RealWorld
{
    /// <summary>
    /// Iterator Design Pattern
    /// </summary>

    public class Program
    {
        public static void Main(string[] args)
        {
            // Build a collection

            Collection collection = new Collection();
            collection[0] = new Item("Item 0");
            collection[1] = new Item("Item 1");
            collection[2] = new Item("Item 2");
            collection[3] = new Item("Item 3");
            collection[4] = new Item("Item 4");
            collection[5] = new Item("Item 5");
            collection[6] = new Item("Item 6");
            collection[7] = new Item("Item 7");
            collection[8] = new Item("Item 8");

            // Create iterator

            Iterator iterator = collection.CreateIterator();

            // Skip every other item

            iterator.Step = 2;

            Console.WriteLine("Iterating over collection:");

            for (Item item = iterator.First();
                !iterator.IsDone; item = iterator.Next())
            {
                Console.WriteLine(item.Name);
            }

            // Wait for user

            Console.ReadKey();
        }
    }
    /// <summary>
    /// A collection item
    /// </summary>

    public class Item
    {
        string name;

        // Constructor

        public Item(string name)
        {
            this.name = name;
        }

        public string Name
        {
            get { return name; }
        }
    }

    /// <summary>
    /// The 'Aggregate' interface
    /// </summary>

    public interface IAbstractCollection
    {
        Iterator CreateIterator();
    }

    /// <summary>
    /// The 'ConcreteAggregate' class
    /// </summary>

    public class Collection : IAbstractCollection
    {
        List<Item> items = new List<Item>();

        public Iterator CreateIterator()
        {
            return new Iterator(this);
        }

        // Gets item count

        public int Count
        {
            get { return items.Count; }
        }

        // Indexer

        public Item this[int index]
        {
            get { return items[index]; }
            set { items.Add(value); }
        }
    }

    /// <summary>
    /// The 'Iterator' interface
    /// </summary>

    public interface IAbstractIterator
    {
        Item First();
        Item Next();
        bool IsDone { get; }
        Item CurrentItem { get; }
    }

    /// <summary>
    /// The 'ConcreteIterator' class
    /// </summary>

    public class Iterator : IAbstractIterator
    {
        Collection collection;
        int current = 0;
        int step = 1;

        // Constructor

        public Iterator(Collection collection)
        {
            this.collection = collection;
        }

        // Gets first item

        public Item First()
        {
            current = 0;
            return collection[current] as Item;
        }

        // Gets next item

        public Item Next()
        {
            current += step;
            if (!IsDone)
                return collection[current] as Item;
            else
                return null;
        }

        // Gets or sets stepsize

        public int Step
        {
            get { return step; }
            set { step = value; }
        }

        // Gets current iterator item

        public Item CurrentItem
        {
            get { return collection[current] as Item; }
        }

        // Gets whether iteration is complete

        public bool IsDone
        {
            get { return current >= collection.Count; }
        }
    }
}


```

**Output**

```powershell
Iterating over collection:
Item 0
Item 2
Item 4
Item 6
Item 8
```

>     Trong đó, `Collection` là một lớp cụ thể của `IAbstractCollection` và chứa một danh sách các đối tượng `Item`. Lớp `Iterator` là một lớp cụ thể của `IAbstractIterator` và được sử dụng để duyệt qua các phần tử của `Collection`.
> 
>     Trong hàm `Main`, một đối tượng `Collection` được khởi tạo và các phần tử được thêm vào. Sau đó, một đối tượng `Iterator` được tạo ra bằng cách gọi phương thức `CreateIterator()` của đối tượng `Collection`. Cuối cùng, chương trình sử dụng đối tượng `Iterator` để duyệt qua các phần tử của `Collection` và in chúng ra màn hình.
> 
> Các phương thức của lớp `Iterator` bao gồm:
> 
> * `First()`: Trả về phần tử đầu tiên của danh sách.
> * `Next()`: Trả về phần tử tiếp theo trong danh sách.
> * `CurrentItem()`: Trả về phần tử hiện tại trong danh sách.
> * `IsDone()`: Kiểm tra xem đã duyệt hết danh sách chưa.
