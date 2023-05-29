# Command Pattern

>    **Command Pattern** (hay còn gọi là Action, Transaction) là một mẫu thiết kế thuộc nhóm hành vi (Behavioral Pattern).

---

<img title="Người ra lệnh cần cung cấp một class đóng gói những mệnh lệnh. Người nhận mệnh lệnh cần phân biệt những interface nào để thực hiện đúng mệnh lệnh." src="https://refactoring.guru/images/patterns/content/command/command-en.png" alt="" data-align="center" style="zoom:100%;">

   Một ví dụ thực tế về Command pattern, trong một nhà hàng ta có người phục vụ và đầu bếp. Người phục vụ sẽ nhận đơn hàng từ khách hàng và chuyển đến cho đầu bếp. 

    Trong ví dụ này, Command pattern có thể được áp dụng để đóng gói yêu cầu đặt món ăn của khách hàng thành một object Command. Người phục vụ sẽ nhận yêu cầu đặt món ăn từ khách hàng và chuyển đến cho đầu bếp thông qua object Command. Đầu bếp sẽ nhận object Command và thực hiện yêu cầu đặt món ăn của khách hàng.

#### # Khái niệm :

>     **Command pattern** là một pattern cho phép bạn chuyển đổi một request thành một object độc lập chứa tất cả thông tin về request. Việc chuyển đổi này cho phép bạn tham số hoá các methods với các yêu cầu khác nhau như log, queue (undo/redo), transtraction.
> 
>     Khái niệm Command Object ( đối tượng ) giống như một class trung gian được tạo ra để lưu trữ các câu lệnh và trạng thái của object tại một thời điểm nào đó.
> 
>     Command dịch ra nghĩa là ra lệnh. Commander nghĩa là chỉ huy, người này không làm mà chỉ ra lệnh cho người khác làm. Như vậy, phải có người nhận lệnh và thi hành lệnh. Người ra lệnh cần cung cấp một class đóng gói những mệnh lệnh. Người nhận mệnh lệnh cần phân biệt những interface nào để thực hiện đúng mệnh lệnh.

 

#### # Sơ đồ UML Command Pattern :

<img title="UML Command pattern" src="https://www.dofactory.com/img/diagrams/net/command.png" alt="" data-align="center">

#### # Các thành phần :

Các lớp và đối tượng tham gia trong mẫu thiết kế này bao gồm:

* **Command (Command) :**
  
  * Khai báo một giao diện để thực hiện một hoạt động.

* **ConcreteCommand (CalculatorCommand) :**
  
  * Xác định một liên kết giữa đối tượng Receiver và một hành động.
  * Triển khai Execute bằng cách gọi các hoạt động tương ứng trên Receiver.

* **Client (CommandApp) :**
  
  * Tạo một đối tượng ConcreteCommand và thiết lập Receiver của nó.
  
  Invoker (User)
  
  * Yêu cầu command thực hiện yêu cầu.

* **Receiver (Calculator) :**
  
  * Biết cách thực hiện các hoạt động liên quan đến việc thực hiện yêu cầu.
  
  

#### # Ta hãy đến với ví dụ :

- **Structural code in C#**

    Đoạn Code cấu trúc này mô tả mẫu thiết kế Command, cho phép lưu trữ các yêu cầu dưới dạng đối tượng, cho phép khách hàng thực thi hoặc phát lại các yêu cầu đó.

```csharp

using System;

namespace Command.Structural
{
    /// <summary>
    /// Command Design Pattern
    /// </summary>

    public class Program
    {
        public static void Main(string[] args)
        {
            // Create receiver, command, and invoker

            Receiver receiver = new Receiver();
            Command command = new ConcreteCommand(receiver);
            Invoker invoker = new Invoker();

            // Set and execute command

            invoker.SetCommand(command);
            invoker.ExecuteCommand();

            // Wait for user

            Console.ReadKey();
        }
    }

    /// <summary>
    /// The 'Command' abstract class
    /// </summary>

    public abstract class Command
    {
        protected Receiver receiver;

        // Constructor

        public Command(Receiver receiver)
        {
            this.receiver = receiver;
        }

        public abstract void Execute();
    }

    /// <summary>
    /// The 'ConcreteCommand' class
    /// </summary>

    public class ConcreteCommand : Command
    {
        // Constructor

        public ConcreteCommand(Receiver receiver) :
            base(receiver)
        {
        }

        public override void Execute()
        {
            receiver.Action();
        }
    }

    /// <summary>
    /// The 'Receiver' class
    /// </summary>

    public class Receiver
    {
        public void Action()
        {
            Console.WriteLine("Called Receiver.Action()");
        }
    }

    /// <summary>
    /// The 'Invoker' class
    /// </summary>

    public class Invoker
    {
        Command command;

        public void SetCommand(Command command)
        {
            this.command = command;
        }

        public void ExecuteCommand()
        {
            command.Execute();
        }
    }
}


```

**Output**

```powershell
Called Receiver.Action()
```

>    Đầu tiên, chúng ta có một `Receiver` class đại diện cho đối tượng nhận yêu cầu và thực hiện hành động. Trong ví dụ này, `Receiver` có một phương thức `Action()` để thực hiện hành động.
> 
>     Tiếp theo, chúng ta có một `Command` abstract class đại diện cho một yêu cầu. `Command` class có một thuộc tính `receiver` để lưu trữ đối tượng nhận yêu cầu và một phương thức trừu tượng `Execute()` để thực hiện yêu cầu.
> 
>     `ConcreteCommand` class kế thừa từ `Command` class và triển khai phương thức `Execute()`. Trong phương thức này, nó gọi phương thức `Action()` của đối tượng `receiver` để thực hiện hành động.
> 
>     `Invoker` class đại diện cho đối tượng gửi yêu cầu. Nó có một thuộc tính `command` để lưu trữ yêu cầu và hai phương thức: `SetCommand()` để thiết lập yêu cầu và `ExecuteCommand()` để thực hiện yêu cầu.
> 
>     Trong hàm `Main()`, chúng ta tạo ra một đối tượng `Receiver`, một đối tượng `ConcreteCommand` với đối tượng `Receiver` được truyền vào như một tham số, và một đối tượng `Invoker`. Sau đó, chúng ta thiết lập yêu cầu cho đối tượng `Invoker` và gọi phương thức `ExecuteCommand()` để thực hiện yêu cầu.
> 
> Khi chạy chương trình, nó sẽ in ra dòng chữ “Called Receiver.Action()” để cho thấy rằng hành động đã được thực hiện.



- **Real-world code in C#**

   Đoạn Code thực tế này mô tả mẫu thiết kế Command được sử dụng trong một máy tính đơn giản với khả năng hoàn tác (undo) và làm lại (redo) không giới hạn. Lưu ý rằng trong C#, từ khóa "operator" là một từ khóa. Đặt ký tự '@' phía trước cho phép sử dụng nó như một định danh.

```csharp
using System;
using System.Collections.Generic;

namespace Command.RealWorld
{
    /// <summary>
    /// Command Design Pattern
    /// </summary>

    public class Program
    {
        public static void Main(string[] args)
        {
            // Create user and let her compute

            User user = new User();

            // User presses calculator buttons

            user.Compute('+', 100);
            user.Compute('-', 50);
            user.Compute('*', 10);
            user.Compute('/', 2);

            // Undo 4 commands

            user.Undo(4);

            // Redo 3 commands

            user.Redo(3);

            // Wait for user

            Console.ReadKey();
        }
    }

    /// <summary>
    /// The 'Command' abstract class
    /// </summary>

    public abstract class Command
    {
        public abstract void Execute();
        public abstract void UnExecute();
    }

    /// <summary>
    /// The 'ConcreteCommand' class
    /// </summary>

    public class CalculatorCommand : Command
    {
        char @operator;
        int operand;
        Calculator calculator;

        // Constructor

        public CalculatorCommand(Calculator calculator,
            char @operator, int operand)
        {
            this.calculator = calculator;
            this.@operator = @operator;
            this.operand = operand;
        }

        // Gets operator

        public char Operator
        {
            set { @operator = value; }
        }

        // Get operand

        public int Operand
        {
            set { operand = value; }
        }

        // Execute new command

        public override void Execute()
        {
            calculator.Operation(@operator, operand);
        }

        // Unexecute last command

        public override void UnExecute()
        {
            calculator.Operation(Undo(@operator), operand);
        }

        // Returns opposite operator for given operator

        private char Undo(char @operator)
        {
            switch (@operator)
            {
                case '+': return '-';
                case '-': return '+';
                case '*': return '/';
                case '/': return '*';
                default:
                    throw new
             ArgumentException("@operator");
            }
        }
    }

    /// <summary>
    /// The 'Receiver' class
    /// </summary>

    public class Calculator
    {
        int curr = 0;

        public void Operation(char @operator, int operand)
        {
            switch (@operator)
            {
                case '+': curr += operand; break;
                case '-': curr -= operand; break;
                case '*': curr *= operand; break;
                case '/': curr /= operand; break;
            }
            Console.WriteLine(
                "Current value = {0,3} (following {1} {2})",
                curr, @operator, operand);
        }
    }

    /// <summary>
    /// The 'Invoker' class
    /// </summary>

    public class User
    {
        // Initializers

        Calculator calculator = new Calculator();
        List<Command> commands = new List<Command>();
        int current = 0;

        public void Redo(int levels)
        {
            Console.WriteLine("\n---- Redo {0} levels ", levels);
            // Perform redo operations
            for (int i = 0; i < levels; i++)
            {
                if (current < commands.Count - 1)
                {
                    Command command = commands[current++];
                    command.Execute();
                }
            }
        }

        public void Undo(int levels)
        {
            Console.WriteLine("\n---- Undo {0} levels ", levels);
            
            // Perform undo operations

            for (int i = 0; i < levels; i++)
            {
                if (current > 0)
                {
                    Command command = commands[--current] as Command;
                    command.UnExecute();
                }
            }
        }

        public void Compute(char @operator, int operand)
        {
            // Create command operation and execute it

            Command command = new CalculatorCommand(calculator, @operator, operand);
            command.Execute();

            // Add command to undo list

            commands.Add(command);
            current++;
        }
    }
}


```

**Output**

```powershell
Current value = 100 (following + 100)
Current value =  50 (following - 50)
Current value = 500 (following * 10)
Current value = 250 (following / 2)

---- Undo 4 levels
Current value = 500 (following * 2)
Current value =  50 (following / 10)
Current value = 100 (following + 50)
Current value =   0 (following - 100)

---- Redo 3 levels
Current value = 100 (following + 100)
Current value =  50 (following - 50)
Current value = 500 (following * 10)
```

>     Trong ví dụ này, chúng ta có một `Calculator` class đại diện cho máy tính. `Calculator` class có một phương thức `Operation()` để thực hiện các phép tính cộng, trừ, nhân, chia.
> 
>     `Command` abstract class đại diện cho một yêu cầu. Nó có hai phương thức trừu tượng `Execute()` và `UnExecute()` để thực hiện và hoàn tác yêu cầu.
> 
>     `CalculatorCommand` class kế thừa từ `Command` class và triển khai hai phương thức `Execute()` và `UnExecute()`. Trong phương thức `Execute()`, nó gọi phương thức `Operation()` của đối tượng `calculator` để thực hiện phép tính. Trong phương thức `UnExecute()`, nó gọi phương thức `Operation()` của đối tượng `calculator` với toán tử ngược lại để hoàn tác phép tính.
> 
>     `User` class đại diện cho người dùng sử dụng máy tính. Nó có một thuộc tính `calculator` để lưu trữ đối tượng máy tính, một danh sách `commands` để lưu trữ các yêu cầu và một biến `current` để theo dõi vị trí hiện tại trong danh sách yêu cầu. Nó cũng có ba phương thức: `Redo()` để thực hiện lại các yêu cầu đã hoàn tác, `Undo()` để hoàn tác các yêu cầu và `Compute()` để thực hiện một phép tính mới.
> 
>     Trong hàm `Main()`, chúng ta tạo ra một đối tượng `User` và gọi phương thức `Compute()` nhiều lần để thực hiện các phép tính. Sau đó, chúng ta gọi phương thức `Undo()` để hoàn tác các yêu cầu và gọi phương thức `Redo()` để thực hiện lại các yêu cầu đã hoàn tác.
> 
> Khi chạy chương trình, nó sẽ in ra kết quả của các phép tính và các hoạt động hoàn tác/thực hiện lại.


