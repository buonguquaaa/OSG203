1.
- What What happens when you attempt to use that terminal window?
- Khi chúng ta chạy lệnh xterm thì os sẽ dùng toàn bộ tài nguyên cho cửa sổ terminal để nuôi cửa sổ xterm màu trắng
Khi này thằng terminal – bash sẽ rơi với trạng thái “bị chiếm dụng” hay đợi
Đây là ví dụ
<img width="604" height="303" alt="image" src="https://github.com/user-attachments/assets/5af72c3e-42fd-49ae-88ea-4ac43b766945" />


-Can you access your original terminal window?
Sau khi xoá xterm hoặc bấm ctrl+d thì
Có thể thấy sau khi chạy dòng lệnh xterm – nó sẽ xuất hiện ô cmd màu trắng, và lúc này cmd – bash đã đơ ko thể thêm lệnh.
Đây là sau khi đã end lệnh, mọi thứ quay trở lại hoạt động bình thường.
<img width="599" height="209" alt="image" src="https://github.com/user-attachments/assets/8e7bb806-dec4-47b3-b974-a1424226a3ab" />

b.
- What message do you receive in your original window?
Đây là thông báo mà tôi nhận được khi bấm vào ctrl+z ở cmd đang chạy xterm
<img width="551" height="84" alt="image" src="https://github.com/user-attachments/assets/2544b79b-5281-4ba0-85b7-4ecb526821f1" />

- What happens? (use the xterm window)
Lúc này sẽ không thể thao tác lệnh trong cửa sổ xterm ( màu trắng) nữa
<img width="595" height="313" alt="image" src="https://github.com/user-attachments/assets/292ceeca-9a84-47e0-8f57-768ec8606625" />

- Khi bấm Ctrl + Z, ta đã gửi một tín hiệu sigstop tới tiến trình xterm, nó sẽ ko tắt đi như khi ta dùng ctrl + c mà nó rơi vào trạng thái ‘ngủ đông’. OS sẽ giữ nguyên trạng thái của nó nhưng ko cung cấp tài nguyên CPU để nó xử lí bất kì thao tác nào nữa.
c.
- What is displayed?
- Lúc này thằng terminal sẽ hiển thị danh sách các tiến trình (jobs) đang được quản lí trong session làm việc, cụ thể sẽ hiện ra các nội dung:
+ ID Của job(Ví dụ [1],[2],[3] như bạn có thể thấy ở đầu)
+ Bên cạnh cột ID chính là status của nó, đa số là stopped( vì bạn đang bấm ctrl+z)
+ Các sign ‘+’ và ‘-‘, dấu + ở job (top) chỉ ra đây là tiến trình mặc định, sẽ được đưa trở lại foreground nếu b gõ lệnh fg, dấu – chỉ ra tiến trình sẽ được ưu tiên tiếp theo nếu tiến trình dấu + kết thúc.

- How did you do this?
Đơn giản chỉ cần sử dụng lệnh fg ( viết tắt cho foreground) kết hợp với số thứ tự tiến trình mà bạn buốn back, ở đây đề muốn back về man jobs thì đơn giản chỉ cần chạy lệnh
fg 2 thì nó sẽ ra

Cái man job ( hướng dẫn về job)
- What is displayed now? ( When we quit man jobs)
- Hiện tại nó chỉ show lên 2 tiến trình đang nằm ‘ngủ đông’

Bởi vì ta bấm q cho man jobs ( ta đã kết thúc terminate hoàn toàn của ct man ).
- Which job now has the +?

Như bạn có thể thấy jobs đầu tiên [1] bây giờ đang có dấu cộng
Bởi vì trong Linux nói chung, centos nói riêng thì dấu (+) dùng để kí hiệu cho “current job”, nó là công việc vừa mới tạm dừng hoặc vừa được đưa vào chạy gần nhất
Dấu (-) thì dùng “previous job” (công việc kế trước đó)
Bởi vì ta thực hiện fg1(foreground1) rồi ctrl+z nên hệ thống sẽ đánh dấu thằng job 1 là công việc vừa tương tác gần nhất nên nó có dấu (+)
- Which job resumed? ( If we use fg?)

Câu trả lời là lệnh xterm, nếu ta chỉ nhập fg mà ko có kèm tham số đằng sau, thì nó mặc định sẽ hiểu là fg +, như giải thích bên trên thì dấu + nó sẽ show ra tiến trình vừa tạm dừng là ‘xterm’.
- Which will exit this job. What happened? ( When we type Ctrl + C)
Khi đang chạy lệnh fg mà nhấn Ctrl + C thì tiến trình đó sẽ bị kill ngay lập tức, nôm na đơn giản là thằng xterm đang chạy ở foreground sẽ bị đóng hoàn toàn

Có thể thấy không có job[1] nữa
Ctrl + Z : Tạm dừng ( suspend), tức job vẫn còn đỏ chỉ là đang ngủ đông chờ fg gọi dậy
Ctrl + C : Kill luôn, job ‘ngủ sâu’ mà ko dậy nữa, biến mất khỏi bộ nhớ và danh sách jobs.
-Which job resumed? (When we type fg)

Chỉ có thằng jobs[3] top là sẽ còn. Nên nó sẽ là thằng dấu (+) duy nhất vậy nên khi type fg thì nó sẽ đánh thức top. Do đó nó sẽ vào top
Type q to quit this program. Type jobs, you should see nothing.

Khi ta đã bấm q thì nó sẽ thoát luôn tiến trình top, do đó khi gõ jobs, sẽ ko còn cái nào show ra do các tiến trình đã kết thúc.
d)
-How does this differ from entering xterm without &?
-Đầu tiên cứ thử nhập xterm trước, có thể thấy, khi bạn nhập xterm với ko tham số, thì thằng term (đen) sẽ bị khoá không thể gõ thêm lệnh nào khác cho tới khi cửa số term trắng đóng lại.

- Kế tiếp hãy thử với xterm &

Cửa sổ xterm vẫn mở ra, nhưng term đen sẽ có dấu prompt lệnh và cả term trắng cũng thế, Ta vẫn có thể tiếp tục gõ các lệnh khác trong khi xterm đang chạy
- What is displayed? ( When we type find ~ -empty &)
Khi nhập lệnh đó và ấn enter thì term sẽ hiển thị một thông báo cho biết tiến trình chạy ngầm đã hoàn thành

[1] …  Done ……
Câu lệnh ‘find ~ -empty &’
Find: là lệnh tìm kiếm tập tin/ thư mục trong linux
~: Phạm vi trong home directory( thư mục cá nhân), nó sẽ bắt đầu find từ thư mục này
-empty: nó là một điều kiện lọc (filter) nó sẽ yêu cầu lệnh find chỉ hiển thị ra tập tin hoặc thư mục rỗng.
&: Dấu ‘Và’, nó sẽ yêu cầu hệ thống thực hiện lệnh tìm kiếm này ở chế độ chạy ngầm.
e)
-How the listings of the two xterm jobs differ?
Sự khác biệt giữa 2 thằng xterm này nó nằm ở cột trạng thái.
Một cái Running (đang chạy), một cái stopped
Job chạy ngầm nếu ta nhấn xterm &, còn job stopped là job bị nhấn ctrl _ z
-What do the words “Running” and “Stopped” mean in jobs’ output.

- Running nghĩa là tiến trình đang chạy bình thường dưới nền (background). Nó vẫn đang chiếm tài nguyên và thực thi nhiệm vụ.
-Stopped là tiến trình đã bị tạm dừng hoạt động hoàn toàn, nó vẫn nằm trong bộ nhớ nhưng ko chạy chơi tới khi được đánh thức dậy bằng fg.

- What is output?
Output sẽ là trống

Bởi vì ta đã exit hết tất cả jobs, giờ đây sẽ ko có còn tiến trình nào nữa.
f.
- What is displayed?
Nó sẽ chả hiển thị ra gì hết, nếu còn jobs cũ từ câu trước chưa đóng thì sẽ show ra

-Why do you not see information on the 2 GUI processes?
-Bởi vì lệnh jobs sẽ chỉ liệt kê và quản lí các tiến trình là con của shell hiện tại (tức có thể hiểu là những lệnh đc gõ và khởi chạy trực tiếp từ chính cửa sổ terminal đó.
g.
What happens? (when we type bg top)
Theo lí thuyết thì nó sẽ chuyển trạng thái của thằng top từ stopped sang running tức là nó sẽ chạy dưới dạng là chạy ngầm bg top ( tức là background)
Nhưng mà điều thú vị là nó vẫn ở stopped
Tóm gọn hệ thống cố đưa top vào chạy dưới nền, nhưng vì top yêu cầu quyền truy cập terminal để hiển thị dữu liệu nên nó bị hệ thống tạm dừng lại ngay lập tức.

Has top’s status changed?
Như bạn có thể thấy

Thì thằng top nó vẫn ở trạng thái ‘stopped’, nhưng bây giờ nó đc đánh dấu là một tiến trình chạy ngầm ( có dấu &) thay vì chỉ là một tiến trình bị tạm dừng đơn thuần.

-What happens?(When we run bg xterm)
Câu lệnh đã được thực thi

Nó đã đánh dấu xterm là & tức là đang tiến trình đang chạy ngầm.
Has xterm’s status changed? If so,How?

Như bạn có thể thấy trạng thái của xterm đã đổi từ ‘Stopped’ sang ‘Running’, để ý 2 thứ là cột trạng thái có chữ ‘running’ và cột tên jobs có thêm dấu ‘&’.
2.
-What is the %CPU usage of the top?

Phần trăm CPU được đánh dấu ở chỗ bôi trắng.
- Why is it moving?(when we executes find / -empty)

Vì theo mặc định, top sẽ xếp danh sách dựa trên mức độ sử dụng CPU(%CPU)
Khi lệnh find quét các thư mục khác nhau, mức tiêu thụ CPU của nó thay đổi liên tục, làm vị trí của nó trong bảng thay đổi theo
-As it moves, what happens to its%CPU and %MEM values?

Chỉ số %CPU sẽ tăng vọt lên cao(10-50% hoặc cao hơn) khi nó đang hoạt động tích cực
Chỉ số %MEM(Bộ nhớ) thường sẽ tăng nhẹ hoặc giữ nguyên vì lệnh này chủ yếu tốn tài nguyên xử lí hơn là bộ nhớ
- What happens to the find entry?
Tiến trình find biến mất khỏi danh sách của top điều này là do nó đã thực hiện xong nhiệm vụ tìm kiếm và hệ thống đã giải phóng nó.

2.b
-Why is it moving?
- Về cơ bản, lệnh top sẽ sắp xếp danh sách các tiến trình theo %CPU tiêu thụ. Trong câu lệnh này
Find / -empty 2>/dev/null
Thì thằng find sẽ quét qyuac các thư mục trên ổ đĩa, tài nguyên nó tiêu thụ sẽ thay đổi liên tục, mỗi khi giá trị %CPU của nó thay đổi so với các tiến trình khác, vị trí của nó sẽ được cập nhật lại để đảm bảo thứ tự từ cao xuống thấp.

- As it moves, what happens to its %CPU and %MEM values?
Đầu tiên là về %CPU: Nó sẽ biến động mạnh và thường có xu hướng tăng cao, bởi vì lệnh find chạy thì nó sẽ hoạt động tích cực để tìm các file empty, có thể thấy nó sẽ thường nhảy lên từ 5% tới 20% rồi xuống.
Thứ hai là %MEM: Đa số lệnh chạy chỉ cần sử dụng cpu nên %  sử dụng MEM khá ổn định hoặc nếu có tăng thì sẽ tăng rất nhẹ. Lệnh find tiêu tốn nhiều tài nguyên để xử lí (CPU)_và đọc/ghi hơn là bộ nhớ RAM.
- What happens to the find entry?
Sau khi lệnh find kết thúc, thì bạn có thể thấy find sẽ biến mất hoàn toàn khỏi top

Khi hoàn thành câu lệnh thì OS sẽ giải phóng tiến trình, Top sẽ chỉ hiển thị tiến trình đang hoạt động vì thằng find ko còn chạy nên nó sẽ ko có còn tồn tại trong danh sách quản lí của kernel.
b)
- Why does system have a PID of 1?
Trong Linux, PID có thể coi là mã định danh cho mỗi tiển trình, số 1 là đặc biệt nhất.
Khi máy khởi động và nhân linux(kernel) hoàn tất việc nạp vào bộ nhớ, nó sẽ tạo ra tiến trình đầu tiên duy nhất. Nó được gọi là system
Systemd có thể được coi là “cha đẻ” của các tiến trình khác. Nó chịu trách nhiệm khởi tạo các dịch vụ hệ thống, quản lí việc đăng nhập và duy trì sự hoạt động của máy tính.
Nó là tiến trình đầu tiên thực thi nên nó luôn được gán số thứ tự nhỏ nhất. ( là 1)
- What process is it, what is its PID and what User launched it?

What process is it: TOP
What is its PID: 3000
What user launched it? Nmanhhe+
c)
- What do these three entries represent?
First is VIRT

Next is RES

Final is SHR

VIRT ( Virutal Memory): Nó là tổng lượng bộ nhớ ảo mà tiến trình đang chiếm dụng. Nó bao gồm mọi thứ:
+ Mã chương trình
+ Dữ liệu
+ Các thư viện dùng chung, những phần bộ nhớ được cấp phát nhưng chưa dùng hoặc bị đẩy sang ổ cứng ( swap)
RES ( Resident Memory): Nó đại diện cho bộ nhớ vật lí (RAM) thực tế mà tiến trình đang dùng tại thời điểm hiện tại
SHR (Shared Memory): Lượng bộ nhớ dùng chung với các tiến trình khác.
-What are the values of systemd’s VIRT.RES and SHR in top?

Giá trị của VIRT: 174892
Giá trị của RES: 12268
Giá trị của SHR: 8768
d)
- Compare what you see in the System Monitor Versus what you see in top.

-Điểm giống nhau:
+ Dữ liệu cốt lõi: Cả 2 công cụ đều hiển thị cùng 1 danh sách các tiến trình đang hoạt động trong hệ thống, bao gồm: PID,user,%CPU và %Memory.
+ Khả năng tương tác: Cả 2 đều cho phép bạn sắp xếp dữ liệu và can thiệp( Kill) một tiến trình’
-Điểm Khác Nhau:
-Với (CLI) top ở trên:
+ Trực quan hoá: Chỉ hiển thị số liệu dạng văn bản đơn thuần.
+ Cách điều khiển: Sử dụng phím tắtt ( P,M,N,k,q…)
+Độ chi tiết hệ thống: Hiển thị rõ các trạng thái kernel như PR(priority),NI(Nice) và các kí hiệu trạng thái (S,R,Z)
+Tiêu tốn tài nguyên: Cực kì nhẹ, có thể chạy khi hệ thống đang quá tải
- Với (GUI) System Monitor:
+Trực Quan Hoá: Cung cấp đồ thị thể hiện lịch sử sử dụng tài nguyên theo realtime.
+Cách điều khiển: Sử dụng chuột(Click,kéo thả, menu chuột phải)
+Độ chi tiết hệ thống: Thường ẩn đi các thông số kĩ thuật sâu của nhân (kernel), để giao diện trông gọn gàng, clean hơn.
+Tiêu tốn tài nguyên: Tốn nhiều RAM và CPU để xử lí đồ hoạ.
e)
-In all, which fields are already selected?
-Trong ảnh dưới đây là các trường fields được chọn sẵn

-What fields differ(if any)?
Đối với system monitor: Có những trường rất trực quan mà thằng top nó ko hiển thị mặc định như
+Control Group
+ Disk Read/Write total ( Tổng dung lượng đọc ghi ổ đĩa)
+Session
 +Waiting Channel(Tiến trình đang đợi cái gì)
Đối với lệnh top ( CLI): Tập trung vào các chỉ số kĩ thuật sau của nhân linux như:
+PR ( Priority – độ ưu tiên thực)
 +NI ( Nice value)
+Các giá trị bộ nhớ chia nhỏ như: VIRT,RES,SHR.
-Compare the information about CPU usage, memory and swap history as shown in the GUI to what top tells you
- GUI:
+CPU USAGE: Hiển thị biểu đồ lịch sử ( History) dưới dạng đường kẻ chạy. Có thể xem riêng từng nhân (Core) với màu sắc khác nhau
+Memory & Swap: Cung cấp biểu đồ trực quan giúp thấy rõ tốc độ chiếm dụng RAM và SWAP theo thời gian.
+Tính tiện dụng: Dễ dàng nhận diện các đỉnh điểm(spikes) tài nguyên qua hình ảnh.

-Top(CLI):
+CPU Usage: Chỉ show ra các con số phần trăm tức thời của giây hiện tại. Không có biểu đồ để xem xu hướng tăng giảm trong quá khứ.
+Memory & SWAP: Hiển thị bảng số liệu tĩnh về tổng ( Total), còn trống(Free) và đã sử dụng (Used)
+Tính tiện dụng: Y/c người dùng phải tự ghi nhớ hoặc quan sát các con số nhảy liên tục để nhận ra sự thay đổi.

f.
- Why are no processes shown?
- Vì thời điểm hiện tại, không có tiến trình nào đang được thực hiện bởi tài khoản người dùng có tên là Student. Hệ thống của đang đăng nhập bằng tài khoản nmanhhe201074, do đó khi lọc một user không hoạt động, danh sách sẽ trống rỗng.

- What at are the top processes listed for Student?

Như bạn có thể thấy trong hình.
-Is there a column for Tty now?
- Có, sau khi chọn menu trong f, giờ cột tiêu đề TTY sẽ xuất hiện trên màn hình hiển thị của top

-Which processes are listed that are in a TTY other than
Các tiến trình liệt kê mà khác với dấu? thường là các tiến trình có tính tương tác trực tiếp với người dùng, ví dụ như: bash,top,gnome-terminal-server. Vì các tiến trình hệ thống chạy ngầm (daemons) sẽ hiển thị dấu ‘?’ vì chúng ko gắn liền với 1 cửa sổ term cụ thể nào.
g.
- How do the 2 outputs differ?

Nhìn chung thì cả 2 lệnh ps ở 2 cửa sổ sẽ ko có gì khác nhau nhiều ngoài một vài chi tiết nho nhỏ như số định danh cột PID và cột TTY khác nhau, một bên là pts/0 và một bên là pts/1 vì chúng là 2 thiết bị đầu cuối ảo riêng biệt.
-How does this output differ?

Cũng như trên nó chỉ có một vài điểm khác đa số là PID và TTY
-What does the a option give you?
A option sẽ liệt kê tất cả các tiến trình gắn với một thiet bị đầu cuối (TTY), ngoại trừ các tiến trình “session leaders”
-How does this differ from ps a?
Ps a: hiển thị tiến trình từ mọi terminal, tập trung vào việc ‘ai/ở đâu’ đang chạy
Ps u: thập trung vào thông tin chi tiết( định dạng hướng ngườii dùng), thêm vào các cột như hình dưới đây, b tự tham khảo

-What does the u option do?
Tác dụng của u đó là hiển thị thông tin theo dạng ‘user-oriented’ ( hướng người dùng), cung cấp chi tiết về tài nguyên bộ nhớ và CPu mà tiến trình dang sử dụng
-In the man pages, look up VSZ,RSS,and STAT- what does each mean
-VSZ(Virtual Set Size): Tổng lượng bổ nhớ ảo được cấp phát cho tiến trình (KiB).

-RSS(Resident Set Size): Lượng bộ nhớ vật lí (RAM) thực tế mà tiến trình đang chiếm dụng.

-STAT(Process State): Trạng thái hiện tại của tiến trình

-What do each of these mean
S(Interruptible Sleep): Tiến trình đang ngủ, chờ event( hầu hết các tiến trình đều trạng thái này.
R(Running/Runnable): Tiến trình đang chạy hoặc sẵn sàng chạy.
S(Session leader): Tiến trình trưởng phiên( thường là lệnh bash khởi tạo terminal).
I(Multi-threaded): tiến trình có đa luồng9
+(Foreground): tiến trình đang chạy ẩn, chiếm quyền điều khiểnt term.
h.
-Explain for the gdm processes which spawned which.
* Tiến trình gốc: system (PID1) là tổ tiên, nó sẽ khởi chạy gdm( tiến trình quản lí đăng nhập hệ thống).,
* Sự phân nhánh *: gdm(cha) sẽ sinh ra (spawn) các tiến trình con như gdm-session-worker.
Gdm-session-worker(con): tiến trình này tiếp tục siinh ra thành phần của GUI người dùng như gnome-session-binary và gnome-shell khi b login vào centos9
-What was its history ( in terms of what spawned it)?
Khi bạn nhìn vào dòng lệnh ps axx -H tì bạn hãy nhìn ngược lên các dòng bị thụt lề phía trên nó. “Gia phả của nó” chạy từ dưới lên trên là:
Ps ax -H -> bash -> gnome-terminal-server -> gnome-shell/gnome-session -> gdm/system.
3. Priorities
a.
-What are its priority and NI(nice) values?

GIÁ TRỊ CỦA PR(Priority) là 0 và NI(nice) là -20
Giá trị nice -20 là giá trị thấp nhất, nó là tiến trình ưu tiên.
GIá trị priority thường là 0
Ct cơ bản trong LINUX PR=20+NI nếu NI là -20 thì PR=20-20=0
-What response did you get?
Đây là phản hồi tôi nhận được

-What happens?
Nhận được thông báo lỗi

Bởi đang chạy với quyền user.
-Why did you receive this error?
Lỗi này xuất hiện nguyên tắc bảo mật của linux, một normal user có quyền tăng giá trị NI( làm tiến trình chậm lại và nhường máy tính cho người khác), người dùng ko có quyền giảm giá NI(làm tiến trình chạy nhanh hơn, chiếm quyền ưu tiên)- ngay cả khi họ muốn quay lại mức mặc định ban đầu. CHỉ có root mới có quyền giảm giá trị NI để chiếm ưu tiên của hệ thống.
b.
-What options are available?
Đây là những lựa chọn có sẵn

-What is the range of values available?
Phạm vi giá trị của nó nằm trong khoảng từ -20 tới 19

-20 tương ứng với quyền ưu tiên số 1
19 thì ngươc lại kiểu dân thường.
4. Killing Processes.
a.
-What happens? ( Look at your other terminal window, does your prompt appear? If so, where)?
Cửa sổ xterm sẽ biến mất ngay lập tức mà ko có thông báo nào
Có kèm dấu nhặc lệnh

-What happens?
Tiến trình đó vẫn sống sau khi sử dụng lệnh kill. Signal1 (SIGHUP) ko đủ mạnh để đóng một tiến trình đồ hoạ như xterm nếu nó được tách khỏi terminal control.

-What signal is needed to kill it? Why did -s 9 kill it but not 1?
Dùng signal 9 ( sigkill) để force nó tắt.
SIGNAL 9 (SIGKILL) có thể coi là một tín hiệu ‘tử thần’. Nó gửi trực tới kernel, tiến trình ko thể catch, bỏ quà hay trì hoãn tín hiệu này. Kernel sẽ xoá tiền trình khỏi bộ nhớ ngay lập tức
SIGNAL 1 ( SIGHUP) là tín hiệu hangup. Nó yêu cầu tiến trình kết thúc terminal đóng lại, nhưng nhiều tiênr trình hiện đại đc lập trình để bỏ qua tín hiệu này hoặc dùng nó để reload lại config
-What list of options are there for stopping a process?
Như thể thấy trong MENU có các tuỳ chọn sau

Stop: giống với lệnh kill -STOP. Tiến trình vẫn nằm trong bộ nhớ nhưng bị đóng băng
Continue: giống với kill -CONT. Kích hoạt lại tiến trình đang bị ‘stop’
End: giống với kill -15(sigterm) YÊu cầu tiến trình tự đóng lại với một cách an toàn.
Kill: giống với kill -9 (SIGKILL), buộc tiến trình dừng lập tức, dễ mất dữ liệu nếu chưa save.
b)
- What happens?

Cả 2 cửa sổ xterm đang chạy biến mất cùng lúc vì lệnh này sẽ scan toàn bộ list tiến trình và đóng all những cái tên có chữ “Xterm”
-What is the difference?

Sự khác biệt là thêm dòng y/n, khi bạn thêm chế độ -I ( interacet) nó sẽ cho bạn lựa chọn có xoá tiến trình ko tránh đóng nhầm các tiến trình quan trọng.
-Why might root use killall?
Root thường dùng killall( đặc biệt với các option -u [username]) để nhằm 2 điều
+ dọn dẹp nhanh: đóng toàn bộ chương trình của một người dùng cụ thể khi họ logout hoặc khi tài khoản đó vi phạm chính sách hệ thống…
+ xử lí sự cố: Linux thường dùng để quản lsi server, khi một dịchh vụ như web server tạo ra hàng trăm tiến trình con bị treo, việc dùng killall sẽ nhanh hơn việc tìm và giết từng PID1
 

