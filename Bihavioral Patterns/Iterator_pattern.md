# Iterator Pattern

>    **Iterator Pattern** là một mẫu thiết kế thuộc nhóm hành vi (Behavioral Pattern).

---

<img title="Người ra lệnh cần cung cấp một class đóng gói những mệnh lệnh. Người nhận mệnh lệnh cần phân biệt những interface nào để thực hiện đúng mệnh lệnh." src="https://refactoring.guru/images/patterns/content/iterator/iterator-en.png" alt="" data-align="center" style="zoom:100%;">

   Một ví dụ thực tế gần gũi về Iterator pattern có thể là khi bạn đang duyệt qua một danh sách bài hát trên một ứng dụng nghe nhạc. Bạn có thể sử dụng các nút “next” và “previous” để di chuyển qua lại giữa các bài hát mà không cần biết chi tiết về cách danh sách bài hát được lưu trữ và quản lý. Đây chính là Iterator pattern đang được áp dụng.

#### # Khái niệm :

>    **Iterator pattern** được thiết kế cho phép xử lý nhiều loại tập hợp khác nhau bằng cách truy cập những phần tử của tập hợp với cùng một phương pháp, cùng một cách thức định sẵn, mà không cần phải hiểu rõ về những chi tiết bên trong của những tập hợp này.
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

- **Structural code in java**

    Đoạn Code cnày mô tả mẫu thiết kế Iterator, cung cấp cách để duyệt (lặp) qua một tập hợp các phần tử mà không cần biết chi tiết về cấu trúc nội bộ của tập hợp đó.

```java

// Interface 'Iterator'
public interface Iterator {
    boolean hasNext(); // Kiểm tra xem còn phần tử tiếp theo không
    Object next(); // Lấy phần tử tiếp theo
}

// Interface 'Container'
public interface Container {
    Iterator getIterator(); // Lấy ra một Iterator
}

// Lớp cụ thể triển khai interface 'Container'
public class NameRepository implements Container {
    public String names[] = {"Robert", "John", "Julie", "Lora"};

    @Override
    public Iterator getIterator() {
        return new NameIterator();
    }

    private class NameIterator implements Iterator {
        int index;

        @Override
        public boolean hasNext() {
            if(index < names.length){
                return true;
            }
            return false;
        }

        @Override
        public Object next() {
            if(this.hasNext()){
                return names[index++];
            }
            return null;
        }		
    }
}

// Chương trình chính để kiểm tra
public class Main {
    public static void main(String[] args) {
        NameRepository namesRepository = new NameRepository();

        for(Iterator iter = namesRepository.getIterator(); iter.hasNext();){
            String name = (String)iter.next();
            System.out.println("Name : " + name);
        } 	
    }
}

```
