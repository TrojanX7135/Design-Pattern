# Singleton Pattern

>     **Singleton Pattern**  là một design pattern thuộc nhóm khởi tạo (Creational patterns).

---

<img title="Singleton Pattern" src="https://refactoring.guru/images/patterns/content/singleton/singleton.png" alt="" data-align="center" style="zoom:100%;">

    Bạn có thể hình dung Singleton pattern như một ngôi nhà có một chìa khóa duy nhất. Chìa khóa này được sử dụng để mở cửa và truy cập vào bên trong ngôi nhà. Tất cả mọi người muốn vào ngôi nhà đều phải sử dụng chìa khóa đó và không thể tạo ra chìa khóa mới. Điều này đảm bảo rằng chỉ có một cách duy nhất để truy cập vào ngôi nhà và tất cả mọi người đều phải sử dụng cách đó.



#### Khái niệm :

> **Singleton Pattern** là một trong những **Creational pattern**. Nó cho phép bạn đảm bảo rằng 1 lớp sẽ chỉ có duy nhất 1 instance (đối tượng) và nó cung cấp 1 method cho instance này ở bất cứ đâu trong chương trình.

    **# Singleton giải quyết bài toán nào ?**

    Singleton Pattern giải quyết 2 vấn đề dưới đây cùng 1 lúc:

* **Đảm bảo rằng 1 lớp (class) sẽ chỉ có 1 instance duy nhất**: Sẽ có 1 số trường hợp mà bạn cần kiểm soát việc truy cập đến các tài nguyên dùng chung ví dụ như database hay 1 file nào đó; lúc này bạn cần kiểm soát được số lượng instance mà 1 class đó có.

    _Cách nó hoạt động sẽ như sau: Thử tưởng tượng rằng bạn đã tạo 1 object rồi, tuy nhiên sau đó bạn lại quyết định tạo thêm 1 object mới. Lúc này thay vì việc nhận được 1 object mới thì bạn sẽ nhận về object mà bạn tạo ra lúc trước._

    _Lưu ý rằng hành vi này không thể thực hiện với 1 phương thức khởi tạo thông thường (như sử dụng new), vì nó sẽ luôn trả về 1 object mới._

<img title="Ở đây khách hàng có thể không nhận ra rằng họ đang làm việc với cùng 1 đối tượng" src="https://anywaymeika.files.wordpress.com/2022/03/singleton-comic-1-en.png" alt="" data-align="center" style="zoom:67%;">

* **Cung cấp 1 điểm truy cập global đến instance đó**: Biến global (toàn cục) thường được sử dụng để lưu trữ 1 số đối tượng thiết yếu. Mặc dù nó rất là tiện dụng, nhưng chúng cũng rất không an toàn vì bất cứ đoạn code nào trong chương trình cũng có thể ghi đè nội dung của những biến đó khiến cho ứng dụng của chúng ta bị crash. Singleton cũng giống như biến toàn cục, nó cho phép bạn truy cập đến 1 số object ở bất kỳ đâu trong chương trình, tuy nhiên nó cũng bảo vệ instance đó tránh khỏi việc bị ghi đè bởi code khác.

    _Có 1 cách nhìn khác cho vấn đề này: bạn không muốn phần code giải quyết vấn đề #1 ở trên bị phân tán khắp nơi trong chương trình, source code của mình. Sẽ tốt hơn khi chúng được viết hết trong 1 class đặc biệt là nếu các phần code khác đã phụ thuộc vào nó_



#### Sơ đồ UML Singleton Pattern :

<img title="Singleton Pattern" src="https://www.dofactory.com/img/diagrams/net/Singleton.png" alt="" data-align="center" style="zoom:150%;">

#### Các thành phần:

Các lớp và đối tượng tham gia vào mẫu thiết kế này bao gồm:

* **Singleton (LoadBalancer) :** định nghĩa một hoạt động Instance cho phép khách hàng truy cập vào một phiên bản duy nhất của nó. Instance là một hoạt động của lớp, chịu trách nhiệm tạo và duy trì phiên bản duy nhất của nó.
  
  

#### Ta hãy đến với ví dụ :

    **Ví dụ thực tế :**

>     Singleton có nhiều ví dụ thực tế:
> 
> * 1 đất nước có thể chỉ có 1 chính phủ chính thức. Bất kể ai, cá nhân nào làm việc cho chính phủ thì danh xưng “Chính phủ” vẫn là 1 khái niệm chỉ định chung dùng để chỉ nhóm những người phụ trách. Chính phủ ở đây được xem như 1 ví dụ về Singleton.
> 
> * Khi bạn muốn tăng giảm âm lượng của 1 chiếc điện thoại. Bất kể có gọi từ phần mềm thứ 3, hay thao tác trực tiếp trên phần cứng; thì việc tăng giảm âm lượng cũng đều được thực hiện thông qua 1 phần điều khiển hệ thống. Ta cũng xem lớp điều khiển âm lượng này là 1 singleton
> 
> * Máy in cũng có thể xem là 1 singleton khi nó nhận yêu cầu và xử lý từ mọi người trong hệ thống.



* **Structural code in C#**
  Mã cấu trúc này minh họa mẫu Singleton đảm bảo chỉ có một phiên bản duy nhất (singleton) của lớp có thể được tạo ra.

```csharp

using System;

namespace Singleton.Structural
{
    /// <summary>
    /// Singleton Design Pattern
    /// </summary>

    public class Program
    {
        public static void Main(string[] args)
        {
            // Constructor is protected -- cannot use new

            Singleton s1 = Singleton.Instance();
            Singleton s2 = Singleton.Instance();

            // Test for same instance

            if (s1 == s2)
            {
                Console.WriteLine("Objects are the same instance");
            }

            // Wait for user

            Console.ReadKey();
        }
    }

    /// <summary>
    /// The 'Singleton' class
    /// </summary>

    public class Singleton
    {
        static Singleton instance;

        // Constructor is 'protected'

        protected Singleton()
        {
        }

        public static Singleton Instance()
        {
            // Uses lazy initialization.
            // Note: this is not thread safe.
            if (instance == null)
            {
                instance = new Singleton();
            }

            return instance;
        }
    }
}



```

**Output**

```powershell
Objects are the same instance
```

>     Đây là một ví dụ về cách triển khai mẫu thiết kế Singleton trong C#. Lớp Singleton có một trường tĩnh `instance` để lưu trữ phiên bản duy nhất của lớp Singleton. Hàm tạo của lớp được đánh dấu là `protected` để ngăn chặn việc khởi tạo trực tiếp bằng từ khóa `new`.
> 
>     Lớp cung cấp một phương thức tĩnh `Instance()` để truy cập vào phiên bản duy nhất của lớp Singleton. Phương thức này sử dụng khởi tạo lười (lazy initialization) để tạo phiên bản duy nhất khi nó được gọi lần đầu tiên. Lưu ý rằng cách triển khai này không an toàn với luồng (thread-safe).
> 
>     Trong phương thức `Main`, chúng ta gọi phương thức `Instance()` hai lần để lấy hai phiên bản của lớp Singleton và kiểm tra xem chúng có phải là cùng một phiên bản hay không bằng cách so sánh chúng với nhau.



* **Real-world code in C#**
  Code thực tế này minh họa mẫu Singleton dưới dạng một đối tượng LoadBalancing. Chỉ có một phiên bản duy nhất (singleton) của lớp có thể được tạo ra vì máy chủ có thể tự động bật hoặc tắt và mọi yêu cầu phải đi qua một đối tượng duy nhất có kiến thức về trạng thái của (web) farm.

```csharp
using System;
using System.Collections.Generic;

namespace Singleton.RealWorld
{
    /// <summary>
    /// Singleton Design Pattern
    /// </summary>

    public class Program
    {
        public static void Main(string[] args)
        {
            LoadBalancer b1 = LoadBalancer.GetLoadBalancer();
            LoadBalancer b2 = LoadBalancer.GetLoadBalancer();
            LoadBalancer b3 = LoadBalancer.GetLoadBalancer();
            LoadBalancer b4 = LoadBalancer.GetLoadBalancer();

            // Same instance?

            if (b1 == b2 && b2 == b3 && b3 == b4)
            {
                Console.WriteLine("Same instance\n");
            }

            // Load balance 15 server requests

            LoadBalancer balancer = LoadBalancer.GetLoadBalancer();
            for (int i = 0; i < 15; i++)
            {
                string server = balancer.Server;
                Console.WriteLine("Dispatch Request to: " + server);
            }

            // Wait for user

            Console.ReadKey();
        }
    }

    /// <summary>
    /// The 'Singleton' class
    /// </summary>

    public class LoadBalancer
    {
        static LoadBalancer instance;
        List<string> servers = new List<string>();
        Random random = new Random();

        // Lock synchronization object

        private static object locker = new object();

        // Constructor (protected)

        protected LoadBalancer()
        {
            // List of available servers
            servers.Add("ServerI");
            servers.Add("ServerII");
            servers.Add("ServerIII");
            servers.Add("ServerIV");
            servers.Add("ServerV");
        }

        public static LoadBalancer GetLoadBalancer()
        {
            // Support multithreaded applications through
            // 'Double checked locking' pattern which (once
            // the instance exists) avoids locking each
            // time the method is invoked

            if (instance == null)
            {
                lock (locker)
                {
                    if (instance == null)
                    {
                        instance = new LoadBalancer();
                    }
                }
            }

            return instance;
        }

        // Simple, but effective random load balancer

        public string Server
        {
            get
            {
                int r = random.Next(servers.Count);
                return servers[r].ToString();
            }
        }
    }
}


```

**Output**

```powershell
Same instance

ServerIII
ServerII
ServerI
ServerII
ServerI
ServerIII
ServerI
ServerIII
ServerIV
ServerII
ServerII
ServerIII
ServerIV
ServerII
ServerIV
```

>     Đây là một ví dụ về cách triển khai mẫu thiết kế Singleton trong C# để tạo một đối tượng LoadBalancer. Lớp LoadBalancer có một trường tĩnh `instance` để lưu trữ phiên bản duy nhất của lớp LoadBalancer. Hàm tạo của lớp được đánh dấu là `protected` để ngăn chặn việc khởi tạo trực tiếp bằng từ khóa `new`.
> 
>     Lớp cung cấp một phương thức tĩnh `GetLoadBalancer()` để truy cập vào phiên bản duy nhất của lớp LoadBalancer. Phương thức này sử dụng khởi tạo lười (lazy initialization) và kiểm tra khóa đôi (double-checked locking) để đảm bảo rằng chỉ có một phiên bản duy nhất được tạo ra và phương thức này an toàn với luồng (thread-safe).
> 
>     Trong phương thức `Main`, chúng ta gọi phương thức `GetLoadBalancer()` nhiều lần để lấy các phiên bản của lớp LoadBalancer và kiểm tra xem chúng có phải là cùng một phiên bản hay không bằng cách so sánh chúng với nhau. Sau đó, chúng ta sử dụng thuộc tính `Server` của lớp LoadBalancer để lấy tên máy chủ ngẫu nhiên từ danh sách máy chủ và giả lập việc cân bằng tải 15 yêu cầu máy chủ.


