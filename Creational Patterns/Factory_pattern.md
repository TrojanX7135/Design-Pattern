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


`?` **Trường hợp ta không dùng Factory thì sẽ như thế nào**

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
