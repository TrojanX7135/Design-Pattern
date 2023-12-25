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



* **Structural code in java**
  Mã cấu trúc này minh họa mẫu Singleton đảm bảo chỉ có một phiên bản duy nhất (singleton) của lớp có thể được tạo ra.

```java


public class Singleton {
    // Tạo một thể hiện duy nhất của Singleton
    private static Singleton instance;

    // Làm cho constructor là private để ngăn việc tạo thể hiện mới từ bên ngoài lớp
    private Singleton() {}

    // Phương thức để lấy thể hiện duy nhất của Singleton
    public static Singleton getInstance() {
        // Sử dụng khởi tạo lười biếng.
        // Lưu ý: cách này không an toàn khi sử dụng đa luồng.
        if (instance == null) {
            instance = new Singleton();
        }
        return instance;
    }
}

public class Program {
    public static void main(String[] args) {
        // Constructor là private -- không thể sử dụng new

        Singleton s1 = Singleton.getInstance();
        Singleton s2 = Singleton.getInstance();

        // Kiểm tra xem cả hai thể hiện có phải là cùng một thể hiện không

        if (s1 == s2) {
            System.out.println("Objects are the same instance");
        }

        // Chờ người dùng
    }
}



```

**Output**

```powershell
Objects are the same instance
```

>     Đây là một ví dụ về cách triển khai mẫu thiết kế `Singleton` trong `java`. Lớp Singleton có một trường tĩnh `instance` để lưu trữ phiên bản duy nhất của lớp `Singleton`. Hàm tạo của lớp được đánh dấu là `protected` để ngăn chặn việc khởi tạo trực tiếp bằng từ khóa `new`.
> 
>     Lớp cung cấp một phương thức tĩnh `Instance()` để truy cập vào phiên bản duy nhất của lớp Singleton. Phương thức này sử dụng khởi tạo lười (lazy initialization) để tạo phiên bản duy nhất khi nó được gọi lần đầu tiên. Lưu ý rằng cách triển khai này không an toàn với luồng (thread-safe).
> 
>     Trong phương thức `Main`, chúng ta gọi phương thức `Instance()` hai lần để lấy hai phiên bản của lớp Singleton và kiểm tra xem chúng có phải là cùng một phiên bản hay không bằng cách so sánh chúng với nhau.



* **Real-world code in java**

  Dưới đây là một ví dụ đơn giản về mẫu thiết kế Singleton trong Java, trong đó chúng ta tạo một lớp Database đơn giản

```java
public class Database {
    // Tạo một thể hiện duy nhất của Database
    private static Database instance;

    // Làm cho constructor là private để ngăn việc tạo thể hiện mới từ bên ngoài lớp
    private Database() {}

    // Phương thức để lấy thể hiện duy nhất của Database
    public static synchronized Database getInstance() {
        if (instance == null) {
            instance = new Database();
        }
        return instance;
    }

    // Một phương thức đơn giản để minh họa việc sử dụng Database
    public void query(String sql) {
        System.out.println("Executing SQL query: " + sql);
    }
}

public class Program {
    public static void main(String[] args) {
        // Lấy thể hiện duy nhất của Database
        Database db = Database.getInstance();

        // Sử dụng thể hiện đó để thực hiện một truy vấn
        db.query("SELECT * FROM users");
    }
}



```

Trong ví dụ trên, `Database` là một lớp có một thể hiện duy nhất, và cung cấp một phương thức để lấy thể hiện đó. `Constructor` của `Database` là `private`, nghĩa là bạn không thể tạo một thể hiện mới của `Database` bằng cách sử dụng từ khóa `new` từ bên ngoài lớp. Thay vào đó, bạn phải sử dụng phương thức `getInstance()` để lấy thể hiện duy nhất của `Database`.

Mẫu thiết kế Singleton được sử dụng khi bạn muốn đảm bảo rằng một lớp chỉ có một thể hiện duy nhất, và cung cấp một điểm truy cập toàn cục đến thể hiện đó. Mẫu thiết kế này thường được sử dụng cho các trường hợp như quản lý kết nối cơ sở dữ liệu, cửa sổ đăng nhập, v.v. Trong ví dụ này, chúng ta giả định rằng `Database` là một lớp như vậy. Mặc dù trong thực tế, việc quản lý kết nối cơ sở dữ liệu thường phức tạp hơn nhiều và cần phải xử lý các vấn đề như đa luồng, quản lý tài nguyên, v.v. Nhưng hy vọng ví dụ này sẽ giúp bạn hiểu cơ bản về mẫu thiết kế Singleton.


