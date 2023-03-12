## Tính đóng gói và tính trừu tượng trong lập trình hướng đối tượng
Lập trình hướng đối tượng là một phương pháp lập trình tập trung vào các đối tượng, cũng như mối quan hệ giữa chúng. Tính đóng gói và tính trừu tượng là hai khái niệm quan trọng trong lập trình hướng đối tượng.

### Tính đóng gói (Encapsulation)
Tính đóng gói (Encapsulation) là khả năng giấu thông tin của đối tượng khỏi các đối tượng khác. Trong lập trình hướng đối tượng, đối tượng được coi như một đơn vị độc lập, các trạng thái và hành vi của đối tượng được bảo vệ khỏi sự can thiệp từ các đối tượng khác.

Để đảm bảo tính đóng gói, các thuộc tính và phương thức của đối tượng được định nghĩa với các mức truy cập khác nhau. Các mức truy cập bao gồm:

* Public: Các phương thức và thuộc tính có thể truy cập từ bất kỳ đối tượng nào.
* Protected: Các phương thức và thuộc tính chỉ có thể truy cập từ các lớp con của lớp đó.
* Private: Các phương thức và thuộc tính chỉ có thể truy cập từ bên trong lớp đó.
Việc định nghĩa các mức truy cập cho thuộc tính và phương thức giúp đảm bảo tính đóng gói và tránh các lỗi truy cập không đúng mà không cần kiểm soát chặt chẽ từ bên ngoài.

Để giải thích rõ hơn về tính đóng gói trong lập trình hướng đối tượng, dưới đây là một số ví dụ cụ thể hơn:

***Ví dụ về tính đóng gói trong C++:***

Giả sử bạn đang viết một ứng dụng quản lý sinh viên và muốn lưu trữ thông tin về điểm số của sinh viên. Trong đó, điểm số của sinh viên phải được bảo vệ và chỉ có thể được truy cập hoặc sửa đổi thông qua một phương thức chuyên dụng.

```c
class Student {
private:
    string name;
    int age;
    float score;
public:
    //Hàm khởi tạo
    Student(string n, int a, float s) { 
        name = n;
        age = a;
        score = s;
    }
    //Hàm để set cho thuộc tính score
    void setScore(float s) { 
        score = s;
    }
    //Hàm lấy thuộc tính score
    float getScore() {
        return score;
    }
};

int main() {
    Student s("John", 20, 8.5);
    s.setScore(9.0);
    cout << s.getScore() << endl;
    return 0;
}

Output:  9.0
```

Trong ví dụ này, điểm số của sinh viên được bảo vệ bằng cách đặt nó là một thuộc tính riêng tư (private). Bên ngoài lớp, ta không thể truy cập hoặc sửa đổi thuộc tính này trực tiếp. Thay vào đó, ta cung cấp hai phương thức `setScore()` và `getScore()` để thiết lập và truy xuất điểm số của sinh viên. Điều này giúp đảm bảo rằng thông tin quan trọng như điểm số không bị sửa đổi hoặc truy cập không đúng cách.

### Tính trừu tượng (Abstraction)

Tính trừu tượng (Abstraction) là khả năng trừu tượng hóa các tính năng và hành vi của đối tượng, tách biệt chúng khỏi chi tiết triển khai. Điều này giúp giảm thiểu sự phức tạp của đối tượng, đồng thời tăng tính tái sử dụng và dễ bảo trì.

Tính trừu tượng được đạt được thông qua sử dụng các lớp trừu tượng và phương thức trừu tượng. Lớp trừu tượng là một lớp mà không thể tạo ra các đối tượng từ lớp đó, và nó chỉ định các tính năng chung cho một nhóm lớp. Phương thức trừu tượng là một phương thức chỉ có khai báo mà không có định nghĩa, nó được khai báo trong lớp trừu tượng và sẽ được triển khai trong các lớp con.

***Ví dụ về tính trừu tượng trong C++:***

Giả sử bạn đang viết một ứng dụng về hình học và muốn tính diện tích của một hình tròn và một hình vuông. Trong đó, bạn muốn định nghĩa một lớp trừu tượng `Shape` để đại diện cho một hình học bất kỳ, và một lớp con cho mỗi loại hình học cụ thể. Mỗi lớp con phải triển khai phương thức `getArea()` để tính diện tích của hình đó.

```c
class Shape {
public:
    virtual float getArea() = 0; // Phương thức ảo
};

class Circle : public Shape {
private:
    float radius;
public:
    Circle(float r) {
        radius = r;
    }
    float getArea() {
        return 3.14 * radius * radius;
    }
};

class Square : public Shape {
private:
    float side;
public:
    Square(float s) { 
        side = s;
    }
    float getArea() {
        return side * side;
    }
};

int main() {
Circle c(5);
Square s(6);
cout << "Circle area: " << c.getArea() << endl;
cout << "Square area: " << s.getArea() << endl;
return 0;
}
```

Trong ví dụ này, lớp Shape được định nghĩa là một lớp trừu tượng vì nó không có phương thức thực thi nào. Thay vào đó, nó định nghĩa một phương thức trừu tượng `getArea()` để tính diện tích của hình học bất kỳ. Các lớp con Circle và Square kế thừa từ lớp Shape và triển khai phương thức `getArea()` của riêng mình để tính diện tích của hình tròn và hình vuông.

Tính trừu tượng trong ví dụ này giúp giảm thiểu sự phức tạp của mã và tạo ra một mô hình quản lý được các đối tượng hình học khác nhau trong ứng dụng của bạn. Khi bạn muốn tính diện tích của một hình học bất kỳ, bạn chỉ cần tạo một đối tượng thuộc lớp con tương ứng và gọi phương thức `getArea()` của đối tượng đó.

Tóm lại, tính đóng gói và tính trừu tượng là hai khái niệm quan trọng trong lập trình hướng đối tượng. Tính đóng gói giúp bảo vệ dữ liệu quan trọng của lớp khỏi sự can thiệp bên ngoài, trong khi tính trừu tượng giúp giảm thiểu sự phức tạp của mã và tạo ra một mô hình quản lý được các đối tượng khác nhau trong ứng dụng của bạn.
