# Extract Service 1

Easy

https://extract1-web.wanictf.org/

# Soultion

Đề bài có cho ta file để xem source code. Vào file `main.go` để xem sourccode.

![image](https://user-images.githubusercontent.com/115911041/236623277-c063a538-848c-4b05-b520-99c2d6717805.png)

Ta quan sát thấy có một hàm là `ExtractContent`, hàm này có thể đọc bất cứ file nào bằng cách sử dụng hàm `os.ReadFile`

![image](https://user-images.githubusercontent.com/115911041/236623357-69671550-b3fb-4232-897d-39cc56869b61.png)

Và bởi vì không có filter ở biến `extractTarget` (ở line 38 - 44)

Ở cái website có 1 lỗ hổng tấn công đến `directory traversal`. Các bạn có thể luyện tập và tìm hiểu thêm ở [PortSwigger](https://portswigger.net/web-security/file-path-traversal)

Vậy thì để lấy được flag chúng ta cần that đổi giá trị của tham số `target` thành `../../../../../../flag

`

# Explain

Giá trị biến `target` của `form-data` được nhận và biến `extractTarget` được chuyền đi.

Sau khi combine biến `extractTarget` cùng với đường dẫn `baseDir` với không filter, nó được sử dụng trong hàm `os.RadFile()`.

Vậy là `PATH TRAVERSAL` có lỗ hổng.

Bởi vì `baseDir` là `/tmp/{id value}/`, sau đó đi đến thư mục `root`,đi dến `flag`.

# Example

`baseDir = /tmp/any_id_value/
extracTarget = ../../flag`

`os.ReadFile(filepath.Join(baseDir, extractTarget))` = `os.ReadFile(/flag)`

Và sau khi ta đổi `target` như mình nói ở trên ta đã ra được flag.

![image](https://user-images.githubusercontent.com/115911041/236624686-75733b89-e21a-48d7-842e-c2f0bb12fa41.png)









