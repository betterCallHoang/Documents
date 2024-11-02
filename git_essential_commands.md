# Các lệnh thiết yếu để sử dụng Git
## Khởi tạo user
- Đầu tiên nếu muốn khởi tạo thông tin người dùng có thể dùng 2 câu lệnh dưới đây để cho git biết bạn là ai, user.name và user.email nên để giống với trong Github, ở đây mình lấy ví dụ theo name và email Github của mình luôn. 
```
git config --global user.name "4utumnRain"
git config --global user.email "hoangdepzai0001@gmail.com"
```
**Note**:  `--global` là để khai báo người dùng trong mọi nơi, nếu chỉ muốn 
trong mỗi repo đó thì bỏ `--global` đi.
## Khởi tạo git
---
- `git init` dùng để khởi tạo git trong tại vị trí folder được gõ lệnh đó  đó.
```
git init
```
## Xem trạng thái git
---
```
git status
```
**Example**: Sau khi mình khởi tạo một git trong thư mục của mình, gõ lệnh `git status` được: 
``` 
$ git status
On branch master
Your branch is up to date with 'origin/master'.

Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git restore <file>..." to discard changes in working directory)
        modified:   git_essential_commands.md

no changes added to commit (use "git add" and/or "git commit -a") 
```
Nhìn vào ta có thể hiểu được, git nó sẽ gồm các công đoạn đó là sử dụng lệnh `git add` một file gì đó để theo dõi sự thay đổi của nó (thêm nó vào trạng thái stage), sau đó dùng lệnh `git commit` để lưu lại thay đổi của file đó, sẵn sàng cho việc upload code lên github chẳng hạn.

---
## Thêm biến vào trạng thái stage
- `git add` dùng để adđ một file vào trạng thái stage, sau đó các file đó sẽ được theo dõi.
```
git add [file_name] //dùng để stage 1 file nhất định

git add --all //dùng để stage all file trong folder đó
or
git add -A 
or
git add .
```
**Example**: Mình tạo một file C tên `example_hello.c` có nội dung ví dụ như sau:
```
#include <stdio.h>

int main() {
    printf("Hello World");
    return 0;
}
```
Sau đó dùng lệnh `git add example_hello.c` để đưa file vào trạng thái stage.
Sau đó dùng lệnh `git status` để check:
```
$ git status
On branch master
Your branch is up to date with 'origin/master'.

Changes to be committed:
  (use "git restore --staged <file>..." to unstage)
        new file:   example_hello.c

Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git restore <file>..." to discard changes in working directory)
        modified:   git_essential_commands.md
```
Có thể thấy được file `example_hello.c` đã được stage (được theo dõi những thay đổi của file). Ở đây mình có thể thấy được file hướng dẫn git của mình chưa được stage, mình sẽ dùng lệnh `git add -A` để add tất cả vào trạng thái stage.
```
git commit -m "Bla bla"
```
Dùng để làm checkpoint <br>
Note: Short status flags are:

?? - Untracked files<br>
A - Files added to stage<br>
M - Modified files<br>
D - Deleted files<br>

```
git log
```
Xem history git commit

```
git (command) -help //Dùng để hiện help lệnh cụ thể (chi tiết)

or 

git help --all // Dùng để hiện mô tả tất cả các lệnh
```
### Git branch
```
git branch <name_branch> //Tạo 1 nhánh mới
```

```
git branch //liệt kê các nhánh, nhánh có prefix * là đang xét
```

```
git branch -r // xem nhánh các nhánh từ các remote repo
```


### Git checkout
```
git checkout <branch_name> //Switch tới nhánh branch_name
```


```
git checkout -b <branch_name>
```

Áp dụng tham số -b sẽ tạo một nhánh mới và chuyển ngay đến nhánh đó (kết hợp giữa 2 lệnh `git branch <branch_name> && git checkout <branch_name>`)

```
git checkout -b ＜new-branch＞ ＜existing-branch＞
```

Trong tổng thể, nếu bạn thực hiện lệnh `git branch` thì git sẽ liệt kê hết các branch ở `HEAD` ra, nhưng nếu bạn thực hiện lệnh bên dưới, từ nhánh <existing_branch> bạn lại phân ra 1 nhánh mới, giống như từ 1 thân cây -> nhiều nhánh cây -> nhiều nhánh con.

### Git remote

```
git remote
```

Liệt kê tất cả các remote của các repo mà bạn đang có.

```
git remote -v
```
Giống `git remote` nhưng có thêm link URL
```
git remote add <name> <url>
```
Tạo 1 kết nối mới đến link url, sau khi thực hiện lệnh bạn có thể dùng `name` như là 1 shortcut cho `url`

```
git remote rm <name>
```
Bỏ kết nối tới repo `name`
```
git remote rename <old-name> <new-name>
```
đặt lại tên remote connection

```
git remote show <name>
```
Hiện 1 list nhánh liên quan đến remote `name` đó và các điểm cuối để fetch and push

### Git clone
Git clone sẽ tạo 1 kết nối remote ở repo mà bạn clone về.

### Git push
Dùng để write to the remote repo

```
git push <remote-name> <branch-name>
```

Command trên dùng để update trạng thái hiện tại của `branch-name` lên remote repo `remote-name`

### Git fetch
```
git fetch <remote>
```

Lấy tất cả các nhánh từ repo `remote`

```
git fetch <remote> <branch>
```
Chỉ lấy từ `branch`

```
git fetch --all
```
Lấy tất cả từ các registered remotes 

```
git fetch --dry-run
```
Thực hiện thử chạy lệnh fetch, nó sẽ hiển thị tất cả các hành động trong quá trình fetch nhưng không áp dụng chúng.

```
git fetch origin
```
hiển thị tất cả các nhánh đã được download