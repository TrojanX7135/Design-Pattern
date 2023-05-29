# Facade Pattern

>     **Facade Pattern**  là một design pattern thuộc nhóm cấu trúc ( Structure Design Pattern ). 

---

<img title=" Facade Pattern cung cấp một giao diện chung thân thiện hơn để người dùng có thể dễ dàng sử dụng hệ thống con. Điều này giúp che giấu sự phức tạp của hệ thống con và làm cho nó dễ sử dụng hơn." src="https://images.viblo.asia/2ed6d10d-a495-4846-867b-854c50eb3a9d.png" alt="" data-align="center" style="zoom:100%;">

    Một ví dụ thực tế về việc sử dụng Facade Pattern có thể là khi bạn đến một khách sạn. Khi bạn đến khách sạn, bạn không cần phải liên hệ trực tiếp với từng bộ phận khác nhau của khách sạn để đặt phòng, đặt món ăn, yêu cầu dịch vụ giặt ủi,… Thay vào đó, bạn chỉ cần liên hệ với lễ tân và họ sẽ giúp bạn giải quyết tất cả các yêu cầu đó. Trong trường hợp này, lễ tân chính là một “Facade” giúp che giấu sự phức tạp của các bộ phận khác nhau trong khách sạn và cung cấp cho bạn một giao diện đơn giản để sử dụng các dịch vụ của khách sạn.

#### # Khái niệm :

>     **Facade Pattern** là một mẫu thiết kế thuộc nhóm cấu trúc
> 
>     Facade Pattern cung cấp cho chúng ta một giao diện chung đơn giản thay cho một nhóm các giao diện có trong một hệ thống con (subsystem). Facade Pattern định nghĩa một giao diện ở cấp độ cao hơn để giúp cho người dùng có thể dễ dàng sử dụng hệ thống con này.
> 
>     Facade Pattern cho phép các đối tượng truy cập trực tiếp giao diện chung này để giao tiếp với các giao diện có trong hệ thống con. Mục tiêu là che giấu các hoạt động phức tạp bên trong hệ thống con, làm cho hệ thống con dễ sử dụng hơn.

 

#### # Sơ đồ UML Facade Pattern :

<img title="UML Facade pattern" src="https://www.dofactory.com/img/diagrams/net/facade.png" alt="" data-align="center">

#### 

#### # Các thành phần:

Các lớp và đối tượng tham gia trong mẫu thiết kế này bao gồm:

* **Facade (MortgageApplication) :**
  
  * Biết rõ các lớp con hệ thống con nào chịu trách nhiệm cho một yêu cầu.
  
  * Chuyển giao yêu cầu của khách hàng cho các đối tượng hệ thống con thích hợp.

* **Subsystem classes (Bank, Credit, Loan) :**
  
  * Triển khai chức năng của hệ thống con.
  
  * Xử lý công việc được giao bởi đối tượng Facade.
  
  * Không biết về đối tượng facade và không giữ tham chiếu đến nó.
    
    

#### # Ta hãy đến với ví dụ :

- **Structural code in C#**

    Đoạn Code cấu trúc này mô tả mẫu thiết kế Facade, cung cấp một giao diện đơn giản và đồng nhất cho một hệ thống con lớn gồm nhiều lớp.

```csharp

using System;

namespace Facade.Structural
{
    /// Facade Design Pattern

    public class Program
    {
        public static void Main(string[] args)
        {
            Facade facade = new Facade();

            facade.MethodA();
            facade.MethodB();

            Console.ReadKey();
        }
    }

    public class SubSystemOne
    {
        public void MethodOne()
        {
            Console.WriteLine(" SubSystemOne Method");
        }
    }

    public class SubSystemTwo
    {
        public void MethodTwo()
        {
            Console.WriteLine(" SubSystemTwo Method");
        }
    }

    public class SubSystemThree
    {
        public void MethodThree()
        {
            Console.WriteLine(" SubSystemThree Method");
        }
    }

    public class SubSystemFour
    {
        public void MethodFour()
        {
            Console.WriteLine(" SubSystemFour Method");
        }
    }

    public class Facade
    {
        SubSystemOne one;
        SubSystemTwo two;
        SubSystemThree three;
        SubSystemFour four;

        public Facade()
        {
            one = new SubSystemOne();
            two = new SubSystemTwo();
            three = new SubSystemThree();
            four = new SubSystemFour();
        }

        public void MethodA()
        {
            Console.WriteLine("\nMethodA() ---- ");
            one.MethodOne();
            two.MethodTwo();
            four.MethodFour();
        }

        public void MethodB()
        {
            Console.WriteLine("\nMethodB() ---- ");
            two.MethodTwo();
            three.MethodThree();
        }
    }
}


/*

///Nếu không dùng Facade


public static void Main(string[] args)
{
    SubSystemOne one = new SubSystemOne();
    SubSystemTwo two = new SubSystemTwo();
    SubSystemThree three = new SubSystemThree();
    SubSystemFour four = new SubSystemFour();

    Console.WriteLine("\nMethodA() ---- ");
    one.MethodOne();
    two.MethodTwo();
    four.MethodFour();

    Console.WriteLine("\nMethodB() ---- ");
    two.MethodTwo();
    three.MethodThree();

    Console.ReadKey();
}
*/



```

**Output**

```powershell
MethodA() ----
SubSystemOne Method
SubSystemTwo Method
SubSystemFour Method

MethodB() ----
SubSystemTwo Method
SubSystemThree Method
```

>     Trong ví dụ này, chúng ta có 4 lớp hệ thống con là `SubSystemOne`, `SubSystemTwo`, `SubSystemThree` và `SubSystemFour`. Mỗi lớp này đều có một phương thức riêng biệt.
> 
>     Lớp `Facade` được tạo ra để che giấu sự phức tạp của các lớp hệ thống con. Nó khởi tạo các đối tượng của các lớp hệ thống con và cung cấp hai phương thức là `MethodA` và `MethodB` để người dùng có thể gọi. Các phương thức này sẽ gọi các phương thức của các lớp hệ thống con một cách đơn giản hơn.
> 
>     Trong chương trình chính, chúng ta khởi tạo một đối tượng của lớp `Facade` và gọi hai phương thức `MethodA` và `MethodB`. Nhờ có lớp `Facade`, người dùng không cần phải quan tâm đến việc gọi các phương thức của các lớp hệ thống con một cách trực tiếp.



- **Real-world code in C#**

   Đoạn Code thực tế này mô tả mẫu thiết kế Facade dưới dạng đối tượng MortgageApplication, cung cấp một giao diện đơn giản cho một hệ thống con lớn gồm các lớp đo lường khả năng tín dụng của một người đăng ký.

```csharp
using System;

namespace Facade.RealWorld
{
    /// <summary>
    /// Facade Design Pattern
    /// </summary>

    public class Program
    {
        public static void Main(string[] args)
        {
            // Facade

            Mortgage mortgage = new Mortgage();

            // Evaluate mortgage eligibility for customer

            Customer customer = new Customer("Ann McKinsey");
            bool eligible = mortgage.IsEligible(customer, 125000);

            Console.WriteLine("\n" + customer.Name +
                    " has been " + (eligible ? "Approved" : "Rejected"));

            Console.ReadKey();
        }
    }

    /// The 'Subsystem ClassA' class

    public class Bank
    {
        public bool HasSufficientSavings(Customer c, int amount)
        {
            Console.WriteLine("Check bank for " + c.Name);
            return true;
        }
    }

    /// The 'Subsystem ClassB' class

    public class Credit
    {
        public bool HasGoodCredit(Customer c)
        {
            Console.WriteLine("Check credit for " + c.Name);
            return true;
        }
    }

    /// The 'Subsystem ClassC' class

    public class Loan
    {
        public bool HasNoBadLoans(Customer c)
        {
            Console.WriteLine("Check loans for " + c.Name);
            return true;
        }
    }

    /// Customer class

    public class Customer
    {
        private string name;

        // Constructor

        public Customer(string name)
        {
            this.name = name;
        }

        public string Name
        {
            get { return name; }
        }
    }

    /// The 'Facade' class

    public class Mortgage
    {
        Bank bank = new Bank();
        Loan loan = new Loan();
        Credit credit = new Credit();

        public bool IsEligible(Customer cust, int amount)
        {
            Console.WriteLine("{0} applies for {1:C} loan\n",
                cust.Name, amount);

            bool eligible = true;

            // Check creditworthyness of applicant

            if (!bank.HasSufficientSavings(cust, amount))
            {
                eligible = false;
            }
            else if (!loan.HasNoBadLoans(cust))
            {
                eligible = false;
            }
            else if (!credit.HasGoodCredit(cust))
            {
                eligible = false;
            }

            return eligible;
        }
    }
}



```

**Output**

```powershell
Ann McKinsey applies for $125,000.00 loan

Check bank for Ann McKinsey
Check loans for Ann McKinsey
Check credit for Ann McKinsey

Ann McKinsey has been Approved
```

>     Trong ví dụ này, chúng ta có 3 lớp hệ thống con là `Bank`, `Credit` và `Loan`. Mỗi lớp này đều có một phương thức để kiểm tra khả năng vay vốn của khách hàng.
> 
>     Lớp `Mortgage` được tạo ra để che giấu sự phức tạp của các lớp hệ thống con. Nó khởi tạo các đối tượng của các lớp hệ thống con và cung cấp một phương thức là `IsEligible` để người dùng có thể gọi. Phương thức này sẽ gọi các phương thức của các lớp hệ thống con để kiểm tra khả năng vay vốn của khách hàng.
> 
>     Trong chương trình chính, chúng ta khởi tạo một đối tượng của lớp `Mortgage` và gọi phương thức `IsEligible` để kiểm tra khả năng vay vốn của một khách hàng. Nhờ có lớp `Mortgage`, người dùng không cần phải quan tâm đến việc gọi các phương thức của các lớp hệ thống con một cách trực tiếp.
