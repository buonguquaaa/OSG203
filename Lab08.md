LAB08.01


<img width="339" height="58" alt="image" src="https://github.com/user-attachments/assets/308f3227-2e4c-4b92-991d-5de460e94641" />


/1
a,

<img width="477" height="71" alt="image" src="https://github.com/user-attachments/assets/3b00f269-1fd3-4328-9005-d924db227983" />

- Nhập "cat << quit > file1.txt" rồi nhập 1 số nội dung sau đó gõ "quit" để thoát. Thao tác này sẽ tạo ra tệp file1.txt

<img width="489" height="61" alt="image" src="https://github.com/user-attachments/assets/e6cb62a5-8c0c-4c64-b634-93cc44140018" />

- Gõ "ln -s file1.txt file2.txt" để tạo symbolic link, gõ "ln file1.txt file3.txt" để tạo hard link

<img width="714" height="61" alt="image" src="https://github.com/user-attachments/assets/a9fe6535-ebd3-49fd-9848-1c96374f0aa4" />

- So sánh: file1.txt :"-" file thường, file2.txt:"l" symbolic link, file3.txt:"-" hard link

<img width="420" height="108" alt="image" src="https://github.com/user-attachments/assets/13cd7d2a-bbbb-4fda-ae84-ffbb4c03cb51" />

- Cả hai hiển thị giống file1.txt vì đều trỏ tới nội dung đó

<img width="727" height="225" alt="image" src="https://github.com/user-attachments/assets/0bfc6edd-d194-4c8a-afbb-5fb26aa04279" />

- Đổi tên file1 thành file4 bằng lệnh mv file1.txt file4.txt. Kết quả file2.txt bị lỗi (symbolic link hỏng), file3.txt vẫn hoạt động vì symbolic link trỏ tên file, hard link trỏ inode

<img width="419" height="88" alt="image" src="https://github.com/user-attachments/assets/c0db3d9a-f945-4672-bff8-12dda7bce909" />

- file2.txt không đọc được nhưng file3.txt vẫn đọc được

<img width="751" height="324" alt="image" src="https://github.com/user-attachments/assets/19104f29-89f6-4e8c-bd05-370b52896480" />

- Gõ lệnh "mv file4.txt file1.txt". Tạo một thư mục con có tên là "temp", sau đó sao chép "file1.txt" vào "temp/file5.txt". Tiếp theo, trong thư mục chính của bạn, tạo các symbolic link và hard link như trên nhưng tạo các liên kết có tên là "file6.txt" và "file7.txt", cả hai đều trỏ đến "temp/file5.txt". Gõ lệnh "ls –l"

- file2.txt -> file1.txt file6.txt -> temp/file5.txt. Mặc dù cả hai đều trỏ đến cùng nội dung file, nhưng symbolic link không lưu dữ liệu của file, nó chỉ lưu đường dẫn (path) tới file

<img width="744" height="259" alt="image" src="https://github.com/user-attachments/assets/377a0bb5-6b80-4b4c-b396-e7ea7e56e94f" />

- file2.txt (symbolic link) trỏ tới tên file1.txt khi file1.txt bị xóa -> đường dẫn không còn tồn tại


<img width="421" height="86" alt="image" src="https://github.com/user-attachments/assets/077ac2b8-f799-457e-9f1f-bcc5425d9ce6" />

- file3.txt (hard link) chia sẻ inode với file1.txt khi xóa file1.txt → chỉ giảm link count, inode vẫn còn vì file3.txt vẫn trỏ tới nó -> dữ liệu vẫn còn

- file2.txt hiển thị dạng: file2.txt -> file1.txt vì symbolic link chỉ lưu đường dẫn tới file gốc. Khi file1.txt bị xóa, link vẫn còn nhưng đường dẫn đó không còn hợp lệ, nên nó trở thành dangling (broken) symbolic link
