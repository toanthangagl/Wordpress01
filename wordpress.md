# Template của Wordpress

---

## 1.Cấu tạo file nguồn (core file) của Wordpress

**Có 2 Core Wordpress file:**

- wp-config.php: kiểm soát các cài đặt cơ bản của website, bao gồm thông tin kết nối database, Wordpress salts & keys, Wordpress language
- function.php: tập tin này là một trong những tập tin điều hành quan trọng nhất của Wp

**Ngoài ra còn có 2 thư mục trong Wordpress core:**

- wp-content: chứa các plugin, themes, media uploads
- wp-admin: loading Wordpress dashboard, Connection to database, check thông tin user và cấp quyền phù hợp cho user

## 2.Cách thức kết nối tới database.

- Cấu hình database sẽ nằm trong file **wp-config.php**. Trong đó gồm 4 phần cấu hình database:
  - **define(‘DB_NAME’, ‘tên của database’);**
  - **define(‘DB_USER’, ‘tài khoản quản trị database’);**
  - **define(‘DB_PASSWORD’, ‘mật khẩu quản trị database’);**
  - **define(‘DB_HOST’, ‘localhost’);** (MySQL hostname)
  - **define(‘DB_CHARSET’, ‘utf8’);** (Database Charset to use in creating database tables)

## 3.Xử lý vòng lặp (loop) cho bài post cơ bản trong Wordpress theme.

    <?php
        $task__args = array(
            'posts_per_page' => 9,
            'post_type' => 'post',
        );
        $task = new WP_Query( $task__args );
        if ( $task__args -> have_posts() ):
            while( $task__args -> have_posts() ):
                $task__args -> the_post();
                echo '<h1>'. get_the_title() .'</h1>'
            endwhile;
        endif;
    ?>

## 4.Cấu tạo file template - Các file thiết yếu.

- **Cấu trúc file của một template**

  - style.css
  - functions.php
  - index.php
  - header.php
  - footer.php
  - slidebar.php

- **Các file thiết yếu**

  - style.css
  - functions.php
  - index.php

## 5.Nội dung hàm số the_title(), get_the_title() và sự khác nhau giữa chúng

- **Hàm số the_title()**
  **the_title( string $before = '', string $after = '', bool $display = true )**
  - $before : thêm chuỗi trước tiêu đề ()
  - $after : thêm chuỗi sau tiêu đề
  - bool $display: mặc định true sẽ được in ra màn hình. false để ẩn đi
  - return void|string
  - Hàm này thường được dùng để hiện thị tiêu đề trang hoặc bài viết. Nó sẽ tự động lặp và không yêu cầu bất kỳ tham số nào. Nó **chỉ sử dụng trong vòng lặp** để hiển thị tiêu đề của bài viết, trang của hiện tại.
- **Hàm số get_the_title()**
  **get_the_title( int|WP_Post $post )**
  - int|WP_Post: ID của Post hoặc đối tượng WP_Post. Mặc định là $post toàn cục
  - return string
  - Hàm này được sử dụng để lấy tiêu đề của một bài viết hoặc trang và lưu trữ nó trong một biến để thao tác thêm. Nó trả về tiêu đề dưới dạng một chuỗi, cho phép sử dụng theo nhiều cách khác nhau. **Có thể sử dụng bên ngoài vòng lặp**

## 6.Nội dung hàm số get_stylesheet_directory_uri(), get_stylesheet_directory() và sự khác nhau giữa chúng

- **Hàm số get_stylesheet_directory_uri()**

  - return string
  - Hàm trả về URL dưới dạng một chuỗi, cho phép bạn sử dụng nó để liên kết đến các tệp trong thư mục chủ đề, chẳng hạn như stylesheets, images hoặc file JavaScript.

- **Hàm số get_stylesheet_directory()**
  - return string
  - Hàm xuất URL của thư mục theme hiện tại, theo sau là '/style.css'.
  - Hàm này được sử dụng để truy xuất đường dẫn máy chủ **tuyệt đối** của thư mục của theme hiện tại. Nó trả về đường dẫn thư mục dưới dạng một chuỗi, cho phép bạn sử dụng nó để truy cập các tệp trong thư mục chủ đề trên máy chủ.
