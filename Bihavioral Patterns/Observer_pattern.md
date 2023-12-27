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

- **Structural code in java**

    Đoạn Code này mô tả mẫu thiết kế Observer, trong đó các đối tượng đã đăng ký được thông báo và cập nhật khi trạng thái thay đổi.

```java
// Interface 'Observer'
public interface Observer {
    void update(String news);
}

// Lớp 'ConcreteObserver'
public class NewsChannel implements Observer {
    private String news;

    @Override
    public void update(String news) {
        this.news = news;
        System.out.println("NewsChannel received news: " + this.news);
    }
}

// Lớp 'Subject'
public class NewsAgency {
    private String news;
    private List<Observer> observers = new ArrayList<>();

    public void addObserver(Observer observer) {
        this.observers.add(observer);
    }

    public void removeObserver(Observer observer) {
        this.observers.remove(observer);
    }

    public void setNews(String news) {
        this.news = news;
        for (Observer observer : this.observers) {
            observer.update(this.news);
        }
    }
}

// Chương trình chính để kiểm tra
public class Main {
    public static void main(String[] args) {
        NewsAgency newsAgency = new NewsAgency();
        NewsChannel newsChannel = new NewsChannel();

        newsAgency.addObserver(newsChannel);
        newsAgency.setNews("Breaking news!");
    }
}

```
