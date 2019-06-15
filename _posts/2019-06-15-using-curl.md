---
layout: post
title: Dùng cURL để gọi API?
tags: [tech]
bigimg: /img/June_2019/curl-logo.svg
---

API (Application Programing Interface) là một lớp trung gian giữa Front-end (Web App, Mobile App,..) và Back-end (Services), chúng ta có thể dùng Postman để gọi API hoặc lười hơn hãy dùng cURL command.

## Các Option phổ biến

`-#, --progress-bar`: Thiết lập cho curl hiển thị một progress bar đơn giản thay vì nhiều thông tin liên quan khác.

`-b, --cookie <name=data>`: Hỗ trợ cookie trong request. Nếu không có `=`, thì thay bằng file cookie, (xem `-c`).

`-c, --cookie-jar <file name>`: File dùng để lưu trữ cookie trả về.

`-d, --data <data>`: Gửi kèm dữ liệu trong POST request.

`-f, --fail`: Không trả về  HTML error.

`-F, --form <name=content>`: Submit dữ liệu form.

`-H, --header <header>`: Thiết lập header cho request.

`-i, --include`: Bao gồm header trong output.

`-I, --head`: Chỉ lấy thông tin header.

`-k, --insecure`: Cho phép kết nối **insecure** thành công.

`-L, --location`: Cho phép chuyển trang.

`-o, --output <file>`: Ghi kết quả ra output `<file>` được đặt tên. Có thể dùng `--create-dirs` để tạo đường dẫn.

`-O, --remote-name`: Ghi ra output đến file có tên tương tự ở remote.

`-s, --silent`: Chế độ silent. Dùng với `-S` để chỉ ra errors.

`-v, --verbose`: Cung cấp nhiều thông tin cho việc debug.

`-w, --write-out <format>`: Thiết lập cho curl hiển thị thôn tin trên stdout sau khi hoàn tất transfer. Xem `man curl` để biết chi tiết. Có thể bắt curl thêm newline vào output: `-w "\n"` (can add to `~/.curlrc`).
        
`-X, --request`: Gửi kèm yêu cầu.


## POST

Khi gửi dữ liệu qua POST hoặc PUT request, hai cách định dạng dữ liệu phổ biến được đặc tả trong header (`Content-Type` header) là:
  * `application/json`
  * `application/x-www-form-urlencoded`

Nhiều API có thể chấp nhận cả hai, do đó nếu dùng `curl` tại command line, thì dùng `form urlencoded format` dễ hơn là `json` bởi vì.
  * kiểu json yêu cầu phải có thêm nháy kép
  * curl sẽ gửi `form urlencoded` theo mặc định, do đó nếu gửi json phải set thêm `Content-Type`.


## Dùng curl

Để gửi dữ liệu với POST hoặc PUT requests, có hai lựa chọn:

For sending data with POST and PUT requests, these are common `curl` options:

 * kiểu request
   * `-X POST`
   * `-X PUT`

 * kiểu dữ liệu
  * `-H "Content-Type: application/x-www-form-urlencoded"`
  * `-H "Content-Type: application/json"`
 
* data
  * form urlencoded: `-d "param1=value1&param2=value2"` or `-d @data.txt`
  * json: `-d '{"key1":"value1", "key2":"value2"}'` or `-d @data.json`
  
## Examples

### POST application/x-www-form-urlencoded

`application/x-www-form-urlencoded` là mặc định:

    curl -d "param1=value1&param2=value2" -X POST http://localhost:3000/data

explicit:

    curl -d "param1=value1&param2=value2" -H "Content-Type: application/x-www-form-urlencoded" -X POST http://localhost:3000/data

với file dữ liệu
 
    curl -d "@data.txt" -X POST http://localhost:3000/data

### POST application/json

    curl -d '{"key1":"value1", "key2":"value2"}' -H "Content-Type: application/json" -X POST http://localhost:3000/data
    
với file dữ liệu
 
    curl -d "@data.json" -X POST http://localhost:3000/data

