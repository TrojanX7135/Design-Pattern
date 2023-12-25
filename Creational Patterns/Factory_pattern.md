# Factory Pattern

>     **Factory Pattern**  là một design pattern thuộc nhóm khởi tạo (Creational patterns).

---

<img title="Factory Pattern" src="https://refactoring.guru/images/patterns/content/factory-method/factory-method-en.png?id=cfa26f33dc8473e803fadae0d262100a" alt="" data-align="center" style="zoom:100%;">

#### Khái niệm :

>     Pattern này được sinh ra nhằm mục đích khởi tạo một đối tượng mới mà không cần thiết phải chỉ ra một cách chính xác class nào sẽ được khởi tạo.
> 
>     **Factory Method Pattern** giải quyết vấn đề này bằng cách định nghĩa một factory method cho việc tạo đối tượng, và các lớp con thừa kế có thể override phương thức này để chỉ rõ đối tượng nào sẽ được khởi tạo.

#### Ta hãy đến với ví dụ :

    Một ví dụ về việc sử dụng Factory Pattern trong Java...  

```java

// Interface cho tất cả các loại sản phẩm
public interface Product {
    void use();
}

// Sản phẩm cụ thể 1
public class ConcreteProduct1 implements Product {
    public void use() {
        System.out.println("Using ConcreteProduct1");
    }
}

// Sản phẩm cụ thể 2
public class ConcreteProduct2 implements Product {
    public void use() {
        System.out.println("Using ConcreteProduct2");
    }
}

// Factory để tạo ra sản phẩm
public class ProductFactory {
    public Product createProduct(String type) {
        if ("Product1".equals(type)) {
            return new ConcreteProduct1();
        } else if ("Product2".equals(type)) {
            return new ConcreteProduct2();
        }
        throw new IllegalArgumentException("Invalid product type");
    }
}

// Sử dụng Factory
public class Client {
    public static void main(String[] args) {
        ProductFactory factory = new ProductFactory();
        Product product1 = factory.createProduct("Product1");
        product1.use();  // Output: "Using ConcreteProduct1"
        Product product2 = factory.createProduct("Product2");
        product2.use();  // Output: "Using ConcreteProduct2"
    }
}


```
Trong ví dụ trên, ProductFactory là một Factory, nó tạo ra các đối tượng Product. Các lớp ConcreteProduct1 và ConcreteProduct2 là các lớp cụ thể implement interface Product. Mẫu thiết kế Factory giúp tạo ra các đối tượng mà không cần chỉ định lớp cụ thể của đối tượng đó trong code, giúp tăng tính linh hoạt và tái sử dụng của code.


`?` **Trường hợp ta không dùng Factory thì sẽ như thế nào**

Nếu bạn không sử dụng mẫu thiết kế Factory, bạn sẽ phải tạo đối tượng trực tiếp từ các lớp cụ thể. Điều này có thể dẫn đến việc code của bạn trở nên phụ thuộc vào các lớp cụ thể, làm giảm tính linh hoạt và khả năng tái sử dụng code.

    Dưới đây là ví dụ nếu không dùng factory pattern...

```java
public class Client {
    public static void main(String[] args) {
        Product product1 = new ConcreteProduct1();
        product1.use();  // Output: "Using ConcreteProduct1"
        Product product2 = new ConcreteProduct2();
        product2.use();  // Output: "Using ConcreteProduct2"
    }
}


```

Trong ví dụ trên, có thể thấy rằng chúng ta phải tạo đối tượng trực tiếp từ các lớp ConcreteProduct1 và ConcreteProduct2. Điều này có nghĩa là nếu chúng ta muốn thay đổi loại sản phẩm mà chúng ta tạo (ví dụ: sử dụng một lớp sản phẩm khác như ConcreteProduct3), chúng ta sẽ phải thay đổi code ở nhiều nơi. Điều này làm giảm tính linh hoạt của code và khả năng tái sử dụng. Trái lại, khi sử dụng Factory Design Pattern, chúng ta chỉ cần thay đổi ở một nơi duy nhất: trong Factory. Điều này giúp giữ cho code của chúng ta linh hoạt hơn và dễ dàng tái sử dụng hơn.
