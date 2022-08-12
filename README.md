# Run-Golang-Server-on-Ubuntu
Run Golang Server on Ubuntu

1.ดาวโหลดไฟล์ curl -OL https://golang.org/dl/go1.18.4.linux-amd64.tar.gz

2.แตกไฟล์ sudo tar -C /usr/local -xvf go1.18.4.linux-amd64.tar.gz

3.Set path ที่ profile ใช้คำสั่ง > /etc/profile แล้วเอาคำสั่งไปใส่ที่บรรทัดแรก 
export PATH=$PATH:/usr/local/go/bin

3.2 สร้าง โฟลเด้อ go-test
 
4.สร้างไฟล์ sudo nano main.go
ใส่โค้ด 
package main

import (
    "fmt"
    "net/http"
)

func hello(w http.ResponseWriter, req *http.Request) {

    fmt.Fprintf(w, "hello\n")
}

func headers(w http.ResponseWriter, req *http.Request) {

    for name, headers := range req.Header {
        for _, h := range headers {
            fmt.Fprintf(w, "%v: %v\n", name, h)
        }
    }
}

func main() {

    http.HandleFunc("/hello", hello)
    http.HandleFunc("/headers", headers)

    http.ListenAndServe(":8080", nil)
}

5.จากนั้นใช้คำสั่ง run go >go run main.go &

6.ทดสอบหน้าเว็บด้วยคำสั่ง curl 127.0.0.1:8080/hello


7.เช็ค IP แล้วทดลองเข้าจาก windows
