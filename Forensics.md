
# 1337UP LIVE CTF
Ở cuộc thi **1337UP LIVE CTF** vừa được tổ chức, em đã solved được 2 challange Forensics là **CTF Mind Tricks** và **Logging**. Sau đây em xin trình bày cách làm của mình ở 2 bài trên.

## CTF Mind Tricks

>There's an ongoing investigation into the communications of two potential hackers. As far as I can see, they only shared some music with each other but the feds are convinced something nefarious is going on. Let me know if you can find anything 🔎 
Author: CryptoCat

Challange này cho chúng ta 1 file pcap. Chúng ta sẽ sử dụng **wireshark** để xem file pcap này.

![image](https://hackmd.io/_uploads/HylHOHsvzJl.png)

Như đề bài đã nói là họ đang trao đổi 1 số bản nhạc với nhau. Chúng ta sẽ **Export Objects** để tải về các file được chia sẻ.

![image](https://hackmd.io/_uploads/Syg28ivfye.png)

Ta được file có tên **%5cCapture the Flag Kings.wav**

Sử dụng **AudaCity** rồi chuyển sang **Spectrogram** để phân tích file âm thanh **wav** này.

![image](https://hackmd.io/_uploads/S1lnDivM1l.png)

Quan sát kĩ ta sẽ thấy kì lạ ở phía trên tần số của bài nhạc này, ta kéo dài tần số này xuống phía dưới và nhìn thấy được **Flag**.

![image](https://hackmd.io/_uploads/S1Ib_ovGkl.png)

**Flag: INTIGRITI{hidden_in_music_1337}**

--------------------------------------------------------------------

*Fun fact: Lúc đầu em đã tưởng flag nó nằm ở giữa tần số và em mất hơn nửa ngày chỉnh sửa tần số để tìm flag :sob:*

## Logging

>Any ideas what this log is about? 🤔       
Flag format: INTIGRITI{.*}         
Author: kavigihan

Challange này cho ta 1 file **app.log**. Chúng ta sẽ mở nó lên để quan sát.

![image](https://hackmd.io/_uploads/SJc-2iPzyx.png)

Sau một lúc **google** thì em biết được nó có liên quan tới **SQL**. Nhưng em chỉ biết được như vậy chứ không có thêm được thông tin gì cụ thể hơn.

Sau thêm một lúc mày mò tìm kiếm, em nhớ rằng định dạng của flag nó sẽ có 2 dấu __{__ và __}__, và em đã tìm thấy được 4 dòng có chứa mã ASCII của nó
![image](https://hackmd.io/_uploads/B1bOJ3Df1x.png)
![image](https://hackmd.io/_uploads/Hy_ck2PMkx.png)

Nhận thấy điểm chung giữa 2 dòng trên của mỗi ảnh và 2 dòng dưới của mỗi ảnh, em đã nghĩ rằng các kí tự còn lại sẽ nằm giữa 2 các dòng này và có cùng điểm chung

### Điểm chung 1
Đó là đều nằm trong string **>CHAR(<mã ASCII>)**
Em đã viết source để ghép các kí tự có mã ASCII nằm trong string trên và nằm trên các dòng ở giữa 4 dòng em vừa tìm thấy.

![image](https://hackmd.io/_uploads/Sy9qM2Dfkx.png)   

Nhưng kết quả thì lại không được như mong muốn!

![image](https://hackmd.io/_uploads/HJOaz2DzJg.png)

### Điểm chung 2
Đó là đều nằm trong string **!%3DCHAR(<mã ASCII>)**
Em cũng đã viết source để ghép các kí tự có mã ASCII nằm trong string trên.
![image](https://hackmd.io/_uploads/HyJQQnPzke.png)   
Và em được dòng sau     
![image](https://hackmd.io/_uploads/rJQB7nDMJx.png)   
Thấy **5q1** là **SQL** mà mình đã google được ở trên cộng thêm nhìn dòng này rất giống với các định dạng flag hay gặp nên em đã ghép thêm với định dạng mặc định của giải này là **INTIGRITI{_*}** và thành công solved được bài này.

**Flag: INTIGRITI{5q1_log_analys1s_f0r_7h3_w1n!}**
