- [\[BUỔI 5\] DEV THÌ KHÔNG CHỈ VIẾT CODE](#buổi-5-dev-thì-không-chỉ-viết-code)
- [I. Version Control](#i-version-control)
    - [1. Version Control là gì?](#1-version-control-là-gì)
      - [Các loại Version Control](#các-loại-version-control)
    - [2. Tại sao cần dùng Version Control?](#2-tại-sao-cần-dùng-version-control)
- [II. Các khái niệm về Git](#ii-các-khái-niệm-về-git)
    - [1. Git là gì?](#1-git-là-gì)
      - [Git khác các VCS khác như thế nào?](#git-khác-các-vcs-khác-như-thế-nào)
      - [Git có lợi ích gì?](#git-có-lợi-ích-gì)
    - [2. Các thuật ngữ quan trọng trong Git](#2-các-thuật-ngữ-quan-trọng-trong-git)
        - [2.1. Local Repository và Remote Repository](#21-local-repository-và-remote-repository)
        - [2.2. Commit](#22-commit)
        - [2.3. Branch](#23-branch)
        - [2.4. Pull request](#24-pull-request)
        - [2.5. Checkout](#25-checkout)
        - [2.6. Fetch](#26-fetch)
- [III. Pull Request](#iii-pull-request)
- [IV. UML](#iv-uml)
- [V. Mô hình Class Diagram, Activity Diagram](#v-mô-hình-class-diagram-activity-diagram)



# [BUỔI 5] DEV THÌ KHÔNG CHỈ VIẾT CODE

# I. Version Control
### 1. Version Control là gì?
Version Control System (VCS) là một loại hệ thống giúp chúng ta quản lý các thay đổi trong source code theo dấu thời gian một cách dễ dàng. Một cách dễ hiểu, VCS lưu trữ source code và mọi thay đổi ta thực hiện trên đó dựa theo dòng thời gian, từ đó có thể đưa code quay trở về trạng thái cũ, hoặc kiểm tra những thay đổi đã thực hiện để dễ dàng sửa lỗi, nâng cấp,...
#### Các loại Version Control
- VCS có hai loại:
  - **Centralized Version Control Systems** (VCS tập trung): Tất cả các folder, file của dự án sẽ nằm tập trung tại 1 server lớn duy nhất, các thành viên tham gia dự án có thể lấy code về, chỉnh sửa, sau đó đẩy code trở lại server. VCS tập trung cũng có hạn chế, nếu không may xảy ra sự cố, mà các sao lưu dự phòng chưa được tạo ra tính đến thời điểm đó, bạn sẽ mất toàn bộ lịch sử của dự án đó, ngoại trừ những phiên bản cục bộ mà người dùng có được trên máy tính cá nhân.
  - Khắc phục nhược điểm của VCS thì một loại VCS nữa được đề xuất đó là **Distributed Version Control Systems** (Hệ thống quản lý phiên bản phân tán). Nó giống với CVCS là có một máy chủ, ở đó có Database lưu giữ các phiên bản của file, tuy nhiên khác biệt đó là các máy client (các developer) kết nối vào thì nó không chỉ lấy file mà nó lấy luôn cả hệ thống Database. Điều này có nghĩa là khi Server bị ngắt, các máy client vẫn làm việc bình thường trên Database ở máy trạm, sau đó commit (chuyển) lên Server sau, hoặc Database ở Server bị lỗi thì bất kỳ máy client nào đều có thể phục hồi lại cho Server
### 2. Tại sao cần dùng Version Control?
- Version Control cần dùng vì nó mang lại nhiều lợi ích cho các lập trình viên, đặc biệt là khi làm việc nhóm.
  - Lưu trữ lịch sử của các thay đổi, từ đó có thể khôi phục lại các phiên bản trước đó, so sánh các phiên bản, xem ai đã thực hiện thay đổi gì và khi nào.
  - Hỗ trợ cộng tác giữa các lập trình viên, từ đó có thể chia sẻ mã nguồn, đồng bộ hóa các thay đổi, giải quyết các xung đột, phân quyền và quản lý quy trình phát triển.
  - Tăng hiệu quả và chất lượng của sản phẩm, từ đó có thể kiểm tra và sửa lỗi dễ dàng, phát hiện và ngăn chặn các vấn đề tiềm ẩn, đảm bảo tính nhất quán và bảo mật của mã nguồn.
# II. Các khái niệm về Git
### 1. Git là gì?
- `Git` là một hệ thống VCS (Version Control System) dùng để quản lý và kiểm tra các phiên bản source code khác nhau trong quá trình phát triển.
- Trên `Git`, có thể lưu trạng thái của file khi có nhu cầu dưới dạng lịch sử cập nhật. Vì thế, có thể đưa file đã chỉnh sửa một lần về trạng thái cũ hay có thể hiển thị sự khác biệt ở nơi chỉnh sửa.
- Thêm nữa, khi định ghi đè (overwrite) lên file mới nhất đã chỉnh sửa của người khác bằng file đã chỉnh sửa dựa trên file cũ, thì khi đăng (upload) lên server sẽ hiện ra cảnh cáo. Vì thế, sẽ không xảy ra thất bại về việc đã ghi đè lên nội dung chỉnh sửa của người khác mà không hề hay biết.
> Vốn là một VCS nên Git cũng ghi nhớ lại toàn bộ lịch sử thay đổi của source code trong dự án. Lập trình viên nào sửa file, thêm dòng code tại đâu, xóa dòng code ở hàng nào… đều được Git ghi nhận và lưu trữ lại.

#### Git khác các VCS khác như thế nào?
Sự khác biệt chính giữa Git và bất kỳ VCS nào khác (bao gồm Subversion…) là cách Git nghĩ về dữ liệu của nó.
- Các VCS khác như: Subversion, Perforce, Bazaar,... coi thông tin được lưu trữ như là 1 tập hợp các tập tin và các thay đổi được thực hiện trên mỗi tập tin theo thời gian
- Git không nghĩ hoặc xử lý dữ liệu theo cách này. Mà thay vào đó, Git coi dữ liệu của nó giống như 1 tập hợp các "ảnh" (snapshot) của một hệ thống tập tin nhỏ. 
- Mỗi khi bạn “commit”, Git sẽ “chụp” và tạo ra một snapshot cùng một tham chiếu tới snapshot đó. Để hiệu quả, nếu các tệp không thay đổi, Git sẽ không lưu trữ lại file — chỉ là một liên kết đến tệp giống file trước đó mà nó đã lưu trữ.

 ![Alt text](image.png)

> Đây là điểm khác biệt quan trọng giữa Git và gần như tất cả các VCS khác. Nó khiến Git phải xem xét lại hầu hết mọi khía cạnh của VCS mà hầu hết các hệ thống khác đã sao chép từ thế hệ trước. Điều này làm cho Git giống như một hệ thống tệp nhỏ với một số công cụ cực kỳ mạnh mẽ được xây dựng trên nó, thay vì chỉ đơn giản là một VCS. 

#### Git có lợi ích gì?
- Các dự án thực tế thường có nhiều lập trình viên làm việc song song. Vì vậy, Git sẽ đảm bảo không có xung đột code giữa các lập trình viên.
- Các yêu cầu trong các dự án thường sẽ thay đổi thường xuyên. Vì vậy, một VCS cho phép các dev có thể revert và quay lại phiên bản cũ hơn của code.
- Đôi khi một số dự án đang được chạy song song liên quan đến cùng một cơ sở code. Trong trường hợp như vậy, khái niệm `phân nhánh` trong Git là rất quan trọng.
  - Dễ sử dụng, thao tác nhanh, gọn, lẹ và rất an toàn.
  - Dễ dàng kết hợp các phân nhánh (branch), có thể giúp quy trình làm việc code theo nhóm đơn giản hơn rất nhiều.
  - Chỉ cần clone mã nguồn từ kho chứa hoặc clone một phiên bản thay đổi nào đó từ kho chứa, hoặc một nhánh nào đó từ kho chứa là bạn có thể làm việc ở mọi lúc mọi nơi.
  - Deployment sản phẩm của bạn một cách không thể nào dễ dàng hơn.
### 2. Các thuật ngữ quan trọng trong Git
> Local Repository, Remote Repository, Branch, Commit, Merge, Pull, Push, Clone, Fork.
##### 2.1. Local Repository và Remote Repository
- Trước hết, cần hiểu Repository là gì. `Repository` được hiểu là một kho lưu trữ chứa các files của dự án. Các file đó có thể là code, hình ảnh, âm thanh hoặc mọi thứ liên quan đến dự án. 
- Có 2 loại repo: 
  - `Local Repository`: là một lại repository nằm trên máy tính của bạn, repository này có nhiêm vụ đồng bộ hóa với remote repository bằng các lệnh của git.
  - `Remote Repository`: là một loại repository được cài đặt trên server chuyên dụng, ví dụ như: GitHub, GitLab, Bitbucket,…
- Khi tự khởi tạo một repository, chúng ta gõ lệnh `$ git init`, lệnh này sẽ tạo ra một thư mục `.git`, đây chính là repository, còn phần code nằm cùng với thư mục .git được gọi là `Working Directory`

Sau khi gõ lệnh `git init`, nếu nhận được thông báo như sau thì việc thực hiện tạo repository đã thành công

```
Initialized empty Git repository in path_to_folder/.git/
```

##### 2.2. Commit
- Là thao tác để lưu lại trạng thái hiện tại trên hệ thống, ghi nhận lại lịch sử các xử lý: thêm, xóa, cập nhật các file hay thư mục trên repository

- Khi thực hiện, repository sẽ ghi lại sự khác biệt giữa lần commit trước so với hiện tại. Chúng được ghi nối tiếp nhau theo thứ tự thời gian -> có thể xem lại lịch sử thay đổi trong quá khứ dựa theo các commit trước đó
- Để thực hiện một commit, bạn sử dụng lệnh `$ git add .` nếu muốn lưu lại tất cả những file đã thay đổi, thêm, xóa,... hoặc `$ git add path_to_file1 path_to_file2` để lưu lại thay đổi chỉ những files mà bạn muốn

- Tiếp theo chạy lệnh` $ git commit -m "Nội dung muốn commit"` để commit các thay đổi đã lưu lại ở trên.
##### 2.3. Branch
- Branch được dùng để phân nhánh và ghi luồng của lịch sử. Bạn có thể dùng Branch để triển khai dự án theo hướng cô lập để không ảnh hưởng đến dự án chính. Tại đây cho phép bạn thử nghiệm các tính năng mới hoặc điều chỉnh, sửa lỗi project.

- Khi khởi tạo Repo hoặc Clone, các thành viên sẽ được tạo lập một branch dùng riêng cho công việc của mình từ branch chính để không làm ảnh hưởng đến công việc của những thành viên khác. Branch riêng này sẽ chứa toàn bộ mã nguồn trong kho.

- Sau khi công việc đã hoàn thành, bạn có thể merge branch vừa tạo vào những branch khác hoặc repository chính bằng cách dùng lệnh `Pull Request`.
##### 2.4. Pull request
- Pull Request là lệnh được dùng để thông báo với mọi người rằng bạn đã đẩy những thay đổi của Branch lên Repository tổng. Khi đó, các thành viên khác có thể chấp nhận hoặc từ chối Request này. Khi lệnh này được mở, bạn và các thành viên có thể xem lại công việc và thảo luận với nhau.

##### 2.5. Checkout
- Sử dụng lệnh `git checkout` để chuyển giữa các branch. Chỉ cần nhập git checkout theo sau là tên của branch bạn muốn chuyển đến hoặc nhập `git checkout master` để trở về branch chính (master branch).

##### 2.6. Fetch
Lệnh git fetch tìm nạp các bản sao và tải xuống tất cả các tệp branch vào máy tính của bạn. Sử dụng nó để lưu các thay đổi mới nhất vào kho lưu trữ của bạn. Nó có thể tìm nạp nhiều branch cùng một lúc.- 


# III. Pull Request

# IV. UML

# V. Mô hình Class Diagram, Activity Diagram
