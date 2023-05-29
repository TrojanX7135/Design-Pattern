# Observer Pattern

>    **Observer Pattern** là một mẫu thiết kế thuộc nhóm hành vi (Behavioral Pattern).

---

<img title="Observer Pattern là một mẫu thiết kế phần mềm mà một đối tượng, gọi là subject, duy trì một danh sách các thành phần phụ thuộc nó, gọi là observer, và thông báo tới chúng một cách tự động về bất cứ thay đổi nào. Đây là dạng pattern hành vi (Behavior Pattern)." src="https://refactoring.guru/images/patterns/content/observer/observer.png" alt="" data-align="center" style="zoom:100%;">

   Một ví dụ thực tế về Observer Pattern có thể là một cửa hàng điện thoại. Giả sử có 10 người trong một khu dân cư muốn mua iPhone 12 ở cửa hàng trung tâm khu dân cư. Nếu cửa hàng không có cơ chế gì thông báo qua điện thoại hoặc email, mỗi người sẽ tới hỏi cửa hàng một vài lần. Câu trả lời là có hoặc chưa có. Nhưng nếu cửa hàng gửi thông báo cho tất cả 10 người về việc có iPhone mới thì sẽ tiện lợi hơn. Trong trường hợp này, cửa hàng chính là subject và những người muốn mua iPhone là observer.

#### # Khái niệm :

>     **Observer Pattern** Định nghĩa mối phụ thuộc một - nhiều giữa các đối tượng để khi mà một đối tượng có sự thay đổi trạng thái, tất cả các thành phần phụ thuộc của nó sẽ được thông báo và cập nhật một cách tự động.
> 
>     Một đối tượng có thể thông báo đến một số lượng không giới hạn các đối tượng khác
> 
>     Chúng giống như việc khi ta đăng ký hay nhấn chuông thông báo 1 kênh Youtube, thì khi kênh đó có video mới (thay đổi trạng thái), chúng sẽ gửi thông báo (một cách tự động) đến chúng ta.

 

#### # Sơ đồ UML Observer Pattern :

<img title="UML Observer pattern" src="https://www.dofactory.com/img/diagrams/net/observer.png" alt="" data-align="center">

#### # Các thành phần :

Các lớp và đối tượng tham gia trong mẫu thiết kế này bao gồm:

* **Subject (Stock) :**
  
  * Biết về các Observer của nó. Bất kỳ số lượng đối tượng Observer nào cũng có thể quan sát một đối tượng Subject.
  * Cung cấp một giao diện để gắn kết và tách các đối tượng Observer.

* **ConcreteSubject (IBM) :**
  
  * Lưu trữ trạng thái quan trọng đối với ConcreteObserver.
  * Gửi thông báo tới các Observer khi trạng thái của nó thay đổi.

* **Observer (IInvestor) :**
  
  * Xác định một giao diện cập nhật cho các đối tượng cần được thông báo về các thay đổi trong một Subject.

* **ConcreteObserver (Investor) :**
  
  * Giữ một tham chiếu đến một đối tượng ConcreteSubject.
  * Lưu trữ trạng thái để duy trì sự nhất quán với Subject.
  * Triển khai giao diện cập nhật Observer để duy trì trạng thái của mình nhất quán với Subject.Triển khai giao diện tạo Iterator để trả về một thể hiện của ConcreteIterator thích hợp.

#### # Ta hãy đến với ví dụ :

- **Structural code in C#**

    Đoạn Code cấu trúc này mô tả mẫu thiết kế Observer, trong đó các đối tượng đã đăng ký được thông báo và cập nhật khi trạng thái thay đổi.

```csharp

using System;
using System.Collections.Generic;

namespace Observer.Structural
{
    /// <summary>
    /// Observer Design Pattern
    /// </summary>

    public class Program
    {
        public static void Main(string[] args)
        {
            // Configure Observer pattern

            ConcreteSubject s = new ConcreteSubject();

            s.Attach(new ConcreteObserver(s, "X"));
            s.Attach(new ConcreteObserver(s, "Y"));
            s.Attach(new ConcreteObserver(s, "Z"));

            // Change subject and notify observers

            s.SubjectState = "ABC";
            s.Notify();

            // Wait for user

            Console.ReadKey();
        }
    }

    /// <summary>
    /// The 'Subject' abstract class
    /// </summary>

    public abstract class Subject
    {
        private List<Observer> observers = new List<Observer>();

        public void Attach(Observer observer)
        {
            observers.Add(observer);
        }

        public void Detach(Observer observer)
        {
            observers.Remove(observer);
        }

        public void Notify()
        {
            foreach (Observer o in observers)
            {
                o.Update();
            }
        }
    }

    /// <summary>
    /// The 'ConcreteSubject' class
    /// </summary>

    public class ConcreteSubject : Subject
    {
        private string subjectState;

        // Gets or sets subject state

        public string SubjectState
        {
            get { return subjectState; }
            set { subjectState = value; }
        }
    }

    /// <summary>
    /// The 'Observer' abstract class
    /// </summary>

    public abstract class Observer
    {
        public abstract void Update();
    }

    /// <summary>
    /// The 'ConcreteObserver' class
    /// </summary>

    public class ConcreteObserver : Observer
    {
        private string name;
        private string observerState;
        private ConcreteSubject subject;

        // Constructor

        public ConcreteObserver(
            ConcreteSubject subject, string name)
        {
            this.subject = subject;
            this.name = name;
        }

        public override void Update()
        {
            observerState = subject.SubjectState;
            Console.WriteLine("Observer {0}'s new state is {1}",
                name, observerState);
        }

        // Gets or sets subject

        public ConcreteSubject Subject
        {
            get { return subject; }
            set { subject = value; }
        }
    }
}


```

**Output**

```powershell
Observer X's new state is ABC
Observer Y's new state is ABC 
Observer Z's new state is ABC
```

>      Trong đó có một lớp trừu tượng `Subject` có các phương thức `Attach`, `Detach` và `Notify` để quản lý các đối tượng `Observer`. Lớp `ConcreteSubject` kế thừa từ lớp `Subject` và có thêm thuộc tính `SubjectState` để lưu trạng thái của đối tượng.
> 
>     Lớp trừu tượng `Observer` có một phương thức trừu tượng `Update` để cập nhật trạng thái của đối tượng. Lớp `ConcreteObserver` kế thừa từ lớp `Observer` và cài đặt phương thức `Update` để cập nhật trạng thái của đối tượng dựa trên trạng thái của đối tượng `Subject`.
> 
>     Trong hàm `Main`, chúng ta tạo ra một đối tượng `ConcreteSubject` và ba đối tượng `ConcreteObserver`. Sau đó, chúng ta gắn ba đối tượng `ConcreteObserver` vào đối tượng `ConcreteSubject` bằng phương thức `Attach`. Khi trạng thái của đối tượng `ConcreteSubject` thay đổi, chúng ta gọi phương thức `Notify` để thông báo cho các đối tượng `ConcreteObserver`. Các đối tượng này sẽ cập nhật trạng thái của chúng dựa trên trạng thái mới của đối tượng `ConcreteSubject`.



- **Real-world code in C#**

   Đoạn Code thực tế này mô tả mẫu thiết kế Observer, trong đó các nhà đầu tư đã đăng ký được thông báo mỗi khi giá cổ phiếu thay đổi.

```csharp
using System;
using System.Collections.Generic;

namespace Observer.RealWorld
{
    /// <summary>
    /// Observer Design Pattern
    /// </summary>

    public class Program
    {
        public static void Main(string[] args)
        {
            // Create IBM stock and attach investors

            IBM ibm = new IBM("IBM", 120.00);
            ibm.Attach(new Investor("Sorros"));
            ibm.Attach(new Investor("Berkshire"));

            // Fluctuating prices will notify investors

            ibm.Price = 120.10;
            ibm.Price = 121.00;
            ibm.Price = 120.50;
            ibm.Price = 120.75;

            // Wait for user

            Console.ReadKey();
        }
    }

    /// <summary>
    /// The 'Subject' abstract class
    /// </summary>

    public abstract class Stock
    {
        private string symbol;
        private double price;
        private List<IInvestor> investors = new List<IInvestor>();

        // Constructor

        public Stock(string symbol, double price)
        {
            this.symbol = symbol;
            this.price = price;
        }

        public void Attach(IInvestor investor)
        {
            investors.Add(investor);
        }

        public void Detach(IInvestor investor)
        {
            investors.Remove(investor);
        }

        public void Notify()
        {
            foreach (IInvestor investor in investors)
            {
                investor.Update(this);
            }

            Console.WriteLine("");
        }

        // Gets or sets the price

        public double Price
        {
            get { return price; }
            set
            {
                if (price != value)
                {
                    price = value;
                    Notify();
                }
            }
        }

        // Gets the symbol

        public string Symbol
        {
            get { return symbol; }
        }
    }

    /// <summary>
    /// The 'ConcreteSubject' class
    /// </summary>

    public class IBM : Stock
    {
        // Constructor

        public IBM(string symbol, double price)
            : base(symbol, price)
        {
        }
    }

    /// <summary>
    /// The 'Observer' interface
    /// </summary>

    public interface IInvestor
    {
        void Update(Stock stock);
    }

    /// <summary>
    /// The 'ConcreteObserver' class
    /// </summary>

    public class Investor : IInvestor
    {
        private string name;
        private Stock stock;

        // Constructor

        public Investor(string name)
        {
            this.name = name;
        }

        public void Update(Stock stock)
        {
            Console.WriteLine("Notified {0} of {1}'s " +
                "change to {2:C}", name, stock.Symbol, stock.Price);
        }

        // Gets or sets the stock

        public Stock Stock
        {
            get { return stock; }
            set { stock = value; }
        }
    }
}


```

**Output**

```powershell
Notified Sorros of IBM's change to $120.10
Notified Berkshire of IBM's change to $120.10

Notified Sorros of IBM's change to $121.00
Notified Berkshire of IBM's change to $121.00

Notified Sorros of IBM's change to $120.50
Notified Berkshire of IBM's change to $120.50

Notified Sorros of IBM's change to $120.75
Notified Berkshire of IBM's change to $120.75
```

>     Trong đó có một lớp trừu tượng `Stock` có các phương thức `Attach`, `Detach` và `Notify` để quản lý các đối tượng `IInvestor`. Lớp `IBM` kế thừa từ lớp `Stock`.
> 
>     Interface `IInvestor` có một phương thức `Update` để cập nhật trạng thái của đối tượng. Lớp `Investor` cài đặt interface `IInvestor` và cài đặt phương thức `Update` để cập nhật trạng thái của đối tượng dựa trên trạng thái của đối tượng `Stock`.
> 
>     Trong hàm `Main`, chúng ta tạo ra một đối tượng `IBM` và hai đối tượng `Investor`. Sau đó, chúng ta gắn hai đối tượng `Investor` vào đối tượng `IBM` bằng phương thức `Attach`. Khi giá cổ phiếu của đối tượng `IBM` thay đổi, chúng ta gọi phương thức `Notify` để thông báo cho các đối tượng `Investor`. Các đối tượng này sẽ cập nhật trạng thái của chúng dựa trên giá cổ phiếu mới của đối tượng `IBM`.
