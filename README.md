# GIT CƠ BẢN

Git là một mô hình quản lý phiên bản phân tán rất thông dụng hiện nay. Là hệ thống giúp mỗi máy tính có thể lưu trữ nhiều phiên bản khác nhau của một mã nguồn được nhân bản (**clone**) từ một kho chứa mã nguồn (**repository**), mỗi thay đổi vào mã nguồn trên máy tính sẽ có thể ủy thác (**commit**) rồi đưa lên máy chủ nơi đặt kho chứa chính.

Cơ chế lưu trữ phiên bản của Git là nó sẽ tạo ra một “*ảnh chụp*” (**snapshot**) trên mỗi tập tin và thư mục sau khi commit, từ đó nó có thể cho phép bạn tái sử dụng lại một ảnh chụp nào đó mà bạn có thể hiểu đó là một phiên bản.

**Github chính là một dịch vụ máy chủ repository** công cộng, mỗi người có thể tạo tài khoản trên đó để tạo ra các kho chứa của riêng mình để có thể làm việc.

## Tạo local repository

## Tạo repository trên Github và làm việc

- Tạo repo trên github: https://github.com/$user-name/$repository
- clone cái kho chứa này về máy bằng lệnh `git clone https://<token>@github.com/$user-name/$repository`.
- Truy cập vào thư mục working tree `cd repositoryName`
- Đưa file này vào Staging Area `git add fileName`
- `git commit -m "text"`
- Đẩy các tập tin đã được commit lên Github `git push origin master`

## Hiểu thêm về Commit và staging area

Staging Area nghĩa là khu vực sẽ lưu trữ những thay đổi của bạn trên tập tin để nó có thể được commit, vì muốn commit tập tin nào thì tập tin đó phải nằm trong Staging Area. Một tập tin khi nằm trong Staging Area sẽ có trạng thái là **Stagged** 

![](https://i.imgur.com/az1TGCh.png)

Commit nghĩa là một hành động để Git lưu lại một bản chụp (snapshot) của các sự thay đổi trong thư mục làm việc, và các tập tin và thư mục được thay đổi đã phải nằm trong Staging Area. Mỗi lần commit nó sẽ được lưu lại lịch sử chỉnh sửa của mã nguồn kèm theo tên và địa chỉ email của người commit. 

Và nếu bạn **muốn đưa tập tin lên repository thì bạn phải commit nó trước** rồi sau đó lệnh `git push origin master` sẽ có nhiệm vụ đưa toàn bộ các tập tin đã được commit lên repository.

**Điều kiện gì để commit một tập tin?**

- Tracked
  - Unmodified: Chưa sửa
  - Modified: Đã chỉnh sửa, không thể commit => đưa về staged: `git add .`
  - Staged: đã sẵn sàng để commit
- Untracked: chỉ mới ở bước thêm tập tin vào thư mục => đưa về staged để có thể commit

Chuyển tập tin từ tracked => untracked: `rm fileName`

Xoá hẳn tập tin ra ở cứng: `rm -f tên_file`

## GIT LOG và UNDO COMMIT

**Xem git log**

`git log` or `git log -p`

Một số tùy chọn xem log sau để tối ưu hơn quy trình đọc log.

- `--since`, `--after`: Xem các lần commit kể từ ngày nhất định.
- `--until`: Xem các lần commit trước từ ngày nhất định.
- `--author`: Xem các lần commit của một người nào đó.
- `--grep`: Lọc các chuỗi trong log và in ra.

`git log --author=binhtamnguyen113@gmail.com --pretty="%s"`

**Lọc với --pretty** : Tham số `--pretty` rất có ích nếu bạn muốn lọc xem một đối tượng nào đó trong lịch sử commit, ví dụ như chỉ xem lời nhắn commit hoặc chỉ xem email của người commit.

Danh sách các `%tag`:

- `%H` –  Commit hash
- `%h` – Abbreviated commit hash
- `%T` – Tree hash
- `%t` – Abbreviated tree hash
- `%P` – Parent hashes
- `%p` – Abbreviated parent hashes
- `%an` – Author name
- `%ae` – Author e-mail
- `%ad` – Author date (format respects the –date=option)
- `%ar` – Author date, relative
- `%cn` – Committer name
- `%ce` – Committer email
- `%cd` – Committer date
- `%cr` – Committer date, relative
- `%s` – Subject

**Undo Commit**

`git commit --amend -m "text prev"`

**Bỏ tập tin ra khỏi Staging Area**

`git reset HEAD tên_file`

## Đánh dấu Commit với Tag

Nếu bạn commit quá nhiều thì sẽ gây khó khăn cho bạn về sau nếu cần xem lại thông tin của lần commit trước mà bạn có thể gắn thẻ đánh dấu (tag) cho mỗi commit và khi cần xem bạn chỉ cần sử dụng lệnh `git show tên_tag` là đã có thông tin rất rõ ràng, ngoài ra nó còn giúp bạn dễ dàng diff (đối chiếu) sau này khi không cần nhớ checksum (dù chỉ cần nhớ vài ký tự đầu tiên) của mỗi commit mà chỉ cần nhớ tag, cũng như có thể tạo thêm branch từ tag để bạn thuận tiện hơn trong việc phân nhánh.

Trong Git có hai kiểu tag chính đó là:

- **Lightweight Tag**: Các tag này chỉ đơn thuần là đánh dấu snapshot của commit.
- **Annotated Tag**: Với tag này, bạn có thể đặt tiêu đề cho tag, và khi xem nó sẽ có thông tin về người tag, ngày tag,….

**Cách tạo Lightweight Tag**

`git tag tên_tag`

**Cách tạo Annotated Tag**

`git tag -a v1.0-an -m "Ra mat phien ban 1.0"`

**Push Tag**
Mặc định lệnh `git push` sẽ không push các tag đã tạo lên repository mà bạn có thể dùng lệnh `git push --tags` để đẩy toàn bộ tag lên repository.

**Nhập tag vào branch**

Branch là **một phân nhánh trong một cây dự án** để bạn sửa mã nguồn mà không ảnh hưởng đến phân nhánh gốc (master).

truy cập vào dữ liệu đã commit thông qua tag kèm theo việc tạo một branch mới với lệnh `git checkout -b tên_branch tên_tag`

Để chuyển về lại master, bạn gõ lệnh `git checkout master`.

Để push cái branch này lên bạn có thể sử dụng lệnh `git push origin version1`

**Sự khác nhau giữa clone, fetch, pulll**

- git clone: Lệnh này sẽ sao chép toàn bộ dữ liệu trên repository và sao chép luôn các thiết lập về repository, tức là nó sẽ tự động tạo một master branch trên máy tính của bạn. Lệnh này chỉ nên sử dụng khi bạn cần tạo mới một Git mới trên máy tính với toàn bộ dữ liệu và thiết lập của một remote repository.
- git pull: Lệnh này sẽ tự động lấy toàn bộ dữ liệu từ remote repository và gộp vào cái branch hiện tại bạn đang làm việc.
- git fetch: Lệnh này sẽ lấy toàn bộ dữ liệu từ remote repository nhưng sẽ cho phép bạn gộp thủ công vào một branch nào đó trên thư mục Git ở máy tính.

## Kỹ thuật phân nhánh

Dùng khi muốn tạo một phiên bản thử nghiệm với mã nguồn đang làm việc trong working tree hiện tại mà không gây ảnh hưởng đến các code hiện tại.

Xem toàn bộ các branch  `git branch`.

Tạo thêm branch, chỉ cần gõ lệnh `git branch tên_brand`

**Checkout một branch**

Checkout ở đây nghĩa là bạn truy cập kiểm tra mã nguồn trong branch đó để làm việc đấy. Để làm việc này, bạn sử dụng lệnh `git checkout tên_branch`.

Để chuyển về branch chính thì gõ `git checkout master`.

`touch fileinbranch01.txt`

`git add .`

`git commit -m "Commit fileinbranch01.txt from branch01"`

`git checkout master`

`ls`

**Gộp dữ liệu từ một branch**

Cần chuyển dữ liệu từ branch01 về master thì sẽ làm lần lượt các lệnh sau:

`git checkout master`

`git merge branch01`

**Xoá branch**

`git branch -d branch01`

**Làm việc với remote branch**

