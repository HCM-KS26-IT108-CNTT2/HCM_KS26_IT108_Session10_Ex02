1.  **Báo cáo phân tích (I/O):** Định nghĩa rõ Input (văn bản thô) và Output (giao diện render chuyên nghiệp).

- Input (văn bản thô) là những ký hiệu và văn bản chỉ toàn chữ và chữ. văn bản thô gồm có những ký tự đặc biệt như #,&,*,... 
- Output (giao diện render chuyên nghiệp) sau khi render lên trang web thì những ký hiệu thô sẽ biến mất mà thay vào đó sẽ là những dòng in đậm, in nghiêng và những gì làm cho trang web đặc sắc hơn thay vì những ký hiệu đặc biệt
 
 
-&gt; **Input (.md, văn bản thô)  →  Trình render Markdown  →  Output (trang HTML đẹp, dễ đọc)**

2. **Source code:** Một file .md chứa đầy đủ: Khối code Python, Bảng so sánh và Task List kiểm tra thiết bị.

- **Khối code python :**

1. **Cập nhật hệ thống:**
```bash
                sudo apt update && sudo upgrade -y
```
2. **Cài đặt thư viện cho cảm biến DHT22:** 

```bash
                sudo apt install -y git python3-pip
                sudo pip3 install Adafruit_DHT
```
3. **Kích hoạt giap tiếp 1-Wire ( nếu dùng  DHT22 )**

     Bật  giao tiếp 1-Wire trên hệ thống 
```bash
                sudo raspi-config       # Chọn: Interface Options >
                                        # 1-wire > Enable
```                              
4. **Kiểm tra module đã được nhận**
   
   Sau khi bật 1-wire, kiểm tra thiết bị
   
   ```bash
               ls / sys/bus/w1/deviceas/  # Kết quả có dạng 28-xxxxxxxx
    ```
5. Chạy thử chương trình đọc cảm biến:

   Tải và chạy file python mẫu
   ```bash
    git clone https://github.com/adafrruit/Adafruit_Python_DHT.git
    cd Adafruit_Python_DHT/examples
    python3 AdafruitDHT.py 22 4     #22: DHT22, 4: GPIO pin
                                    # Nhận kết quả độ ẩm và nhiệt độ
   ```
   6. **Tự động chạy khi khởi động :**
   ```bash
   crontab -e        # Thêm dòng (ví dụ mỗi 5 phút): 
                     */5 * * * * python3 /home/pi/read_dht22.py
   ``` 
   # TASK LIST KIỂM TRA THIẾT BỊ: 


   - [x] Đã cài Raspberry Pi OS và cập nhật bằng `sudo apt update`
- [x] Đã cài thư viện `RPi.GPIO`
- [ ] Cảm biến độ ẩm cắm đúng chân, cắm sâu 5–10 cm vào đất
- [ ] Relay nối đúng chân `PUMP_PIN` (GPIO 17)
- [ ] Máy bơm có nguồn điện riêng, đã kiểm tra dây an toàn
- [ ] Chạy thử `python3 pump_control.py` và thấy in ra độ ẩm
- [ ] Hiệu chỉnh `THRESHOLD_LOW` và `THRESHOLD_HIGH` theo loại đất
- [ ] Ghi lại ngày lắp đặt để theo dõi tuổi thọ cảm biến