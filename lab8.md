![image](https://github.com/user-attachments/assets/b2e4ce78-a562-477e-bab1-807bd521ab9f)

![image](https://github.com/user-attachments/assets/95ebce57-edeb-4640-a255-d3e478427f3d)

![image](https://github.com/user-attachments/assets/3fc335b2-8268-4048-9c32-1cc88c160057)


Ping OK ![image](https://github.com/user-attachments/assets/3d9543a7-f1c5-4291-99d5-236c1143c854)

  ![image](https://github.com/user-attachments/assets/3a01843e-4a82-4d65-b4e9-dd57a795bd04)

![image](https://github.com/user-attachments/assets/8bd09f2d-9c72-4582-b169-98b387cbd619)


ex1. 

![image](https://github.com/user-attachments/assets/d173e112-991a-45ec-90bc-fbc0a90d1170)

exam: 
![image](https://github.com/user-attachments/assets/79055f8a-4297-471e-ac8e-890062ceffaa)


![image](https://github.com/user-attachments/assets/d58e2581-de58-465e-bbf7-39a7f0a93dc5)

iptables -F

Chức năng: Lệnh này "flush" (xóa) tất cả các luật (rules) trong các bảng của iptables.

Mục đích: Dọn dẹp các luật hiện có để bắt đầu thiết lập từ đầu, giúp tránh xung đột hoặc ảnh hưởng từ các luật trước đó.

2. iptables -A INPUT -p icmp --icmp-type echo-request -j ACCEPT

Chức năng: Cho phép các gói tin ICMP "echo-request" (thường dùng cho lệnh ping) được chấp nhận trong chuỗi (chain) INPUT.

Mục đích: Cho phép máy tính nhận các gói tin ping từ bên ngoài để kiểm tra khả năng kết nối, ngay cả khi các loại truy cập khác bị chặn.

3. iptables -A OUTPUT -p icmp --icmp-type echo-reply -j ACCEPT

Chức năng: Cho phép các gói tin ICMP "echo-reply" (hồi đáp ping) được gửi ra ngoài trong chuỗi OUTPUT.

Mục đích: Đảm bảo rằng máy có thể trả lời các yêu cầu ping từ bên ngoài.

4. iptables -A INPUT -m state --state ESTABLISHED,RELATED -j ACCEPT

Chức năng: Cho phép các gói tin vào có trạng thái ESTABLISHED hoặc RELATED trong chuỗi INPUT.

Mục đích: Chấp nhận các kết nối đã được thiết lập và các kết nối liên quan. Giúp duy trì các phiên kết nối hiện tại mà không cần mở lại kết nối mỗi lần.

5. iptables -A OUTPUT -m state --state ESTABLISHED,RELATED -j ACCEPT

Chức năng: Cho phép các gói tin ra có trạng thái ESTABLISHED hoặc RELATED trong chuỗi OUTPUT.

Mục đích: Đảm bảo rằng các kết nối hiện tại có thể tiếp tục gửi và nhận dữ liệu mà không bị gián đoạn.

6. iptables -P INPUT DROP, iptables -P FORWARD DROP, iptables -P OUTPUT DROP

Chức năng: Đặt chính sách mặc định cho các chuỗi INPUT, FORWARD, và OUTPUT là DROP (chặn).

Mục đích: Chặn tất cả các loại truy cập ngoại trừ những gì được phép rõ ràng qua các luật ở trên (ví dụ: chỉ cho phép ping).

7. iptables -A FORWARD -s 10.9.0.0/24 -d 172.16.10.110 -p tcp --dport 80 -j REJECT

Chức năng: Chặn các gói tin từ dải IP 10.9.0.0/24 truy cập vào máy chủ 172.16.10.110 qua cổng 80 (HTTP).

Mục đích: Ngăn không cho các máy tính trên subnet 10.9.0.0/24 truy cập vào máy chủ web nội bộ (iweb), giúp tăng cường bảo mật.

8. iptables -A FORWARD -s 172.16.10.0/24 -d 10.9.0.10 -j REJECT

Chức năng: Chặn các gói tin từ subnet 172.16.10.0/24 đến địa chỉ IP 10.9.0.10.

Mục đích: Ngăn các máy tính trên subnet 172.16.10.0/24 truy cập vào máy chủ badsite, đảm bảo an toàn khi badsite được phát hiện có mã độc.

my code: 

![image](https://github.com/user-attachments/assets/bd544065-df29-464a-bdf8-cf85b7e84614)

exam:

![image](https://github.com/user-attachments/assets/e7fca544-4821-40f6-9e40-0133e4ec7800)


my code  

![image](https://github.com/user-attachments/assets/5522938c-d562-4962-90ac-b18ce67fb2bf)


![image](https://github.com/user-attachments/assets/29215005-14e3-4958-9f70-4ab6e4d88271)








