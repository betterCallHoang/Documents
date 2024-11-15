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
**Example**: Mình tạo một file C tên `example.c` có nội dung ví dụ như sau:
```
#include <stdio.h>

int main() {
    printf("Hello World");
    return 0;
}
```
Sau đó dùng lệnh `git add example.c` để đưa file vào trạng thái stage.
Sau đó dùng lệnh `git status` để check:
```
$ git status
On branch master
Your branch is up to date with 'origin/master'.

Changes to be committed:
  (use "git restore --staged <file>..." to unstage)
        new file:   example.c

Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git restore <file>..." to discard changes in working directory)
        modified:   git_essential_commands.md
```
Có thể thấy được file `example.c` đã được stage (được theo dõi những thay đổi của file). Ở đây mình có thể thấy được file hướng dẫn git .md của mình chưa được stage, mình sẽ dùng lệnh `git add -A` để add tất cả vào trạng thái stage.

---
## Git commit
`git commit` giống như kiểu là 1 save point.

**Example**: Giờ mình muốn commit file .md và file .c của mình, mình sẽ gõ như dưới :
```
git commit -m "First commit of my git tutorial"
```
và sẽ ra kết quả:
```
$ git commit -m "First commit of my git tutorial"
[master aa9eeae] First commit of my git tutorial
 2 files changed, 65 insertions(+), 12 deletions(-)
 create mode 100644 example.c
```
2 file thay đổi ở đây là file .md và file .c của mình, trong đó dòng `create mode 100644 example.c` ý là file .c của mình stage ở chế trạng thái mới tạo, còn file .md trước đó mình đã stage và commit rồi nên không hiện.

---
## Xem lịch sử commit 
Ta dùng:
```
git log
```
**Example**: Mình thử dùng:
```
$ git log
commit aa9eeae50356400ff78b4b4fb345cb2126fb542e (HEAD -> master)
Author: 4utumnRain <hoangdepzai0001@gmail.com>
Date:   Sun Nov 3 05:45:48 2024 +0700

    First commit of my git tutorial

commit ff6c3a20f4a2c35778825b964c4c81d616920df8 (origin/master, origin/HEAD)
Author: hoang_emperor <128159205+hoang-emperor@users.noreply.github.com>
Date:   Thu Sep 14 12:07:18 2023 +0700
```
Nó sẽ hiện các lần mình commit như trên, bởi vì cái tutorial này trước mình cũng làm mà giờ mình làm lại cho dễ hiểu nên bạn sẽ thấy là mình đã commit một lần từ 2023.

---
## Xem các hướng dẫn về lệnh

```
git *command* -help //Dùng để hiện help lệnh cụ thể (chi tiết)
```
For example, ta chạy lệnh `git commit -help` thu được kết quả sau:
```
$ git commit -help
usage: git commit [-a | --interactive | --patch] [-s] [-v] [-u<mode>] [--amend]
                  [--dry-run] [(-c | -C | --squash) <commit> | --fixup [(amend|reword):]<commit>)]
                  [-F <file> | -m <msg>] [--reset-author] [--allow-empty]
                  [--allow-empty-message] [--no-verify] [-e] [--author=<author>]
                  [--date=<date>] [--cleanup=<mode>] [--[no-]status]
                  [-i | -o] [--pathspec-from-file=<file> [--pathspec-file-nul]]
                  [(--trailer <token>[(=|:)<value>])...] [-S[<keyid>]]
                  [--] [<pathspec>...]

    -q, --quiet           suppress summary after successful commit
    -v, --verbose         show diff in commit message template

Commit message options
    -F, --file <file>     read message from file
    --author <author>     override author for commit
    ...
```
kết quả sẽ hiện ra các options cho câu lệnh `commit` của mình (mình đã cắt bớt). 

Còn lệnh `git help --all` này sẽ liệt kê hết các câu lệnh trong git:

```
git help --all // Dùng để hiện mô tả tất cả các lệnh
or 
git help -a 
```
kết quả:

```
$ git help -a
See 'git help <command>' to read about a specific subcommand

Main Porcelain Commands
   add                     Add file contents to the index
   am                      Apply a series of patches from a mailbox
   archive                 Create an archive of files from a named tree
   bisect                  Use binary search to find the commit that introduced a bug
   branch                  List, create, or delete branches
   bundle                  Move objects and refs by archive
   checkout                Switch branches or restore working tree files
   cherry-pick             Apply the changes introduced by some existing commits
   citool                  Graphical alternative to git-commit
   clean                   Remove untracked files from the working tree
   clone                   Clone a repository into a new directory
   ...
```
kết quả đã được xén bớt.
## Tạo ra một nhánh mới tồn tại song song với nhánh chính
Giả sử giờ ta muốn phát triển một tính năng mới trong chương trình của chúng ta mà không muốn bị làm ảnh hưởng đến chương trình hiện tại, ta dùng lệnh `git branch <name_branch>` để tạo một nhánh mới // với nhánh của chương trình chính.
```
git branch <name_branch> //Tạo 1 nhánh mới

git branch //liệt kê các nhánh, nhánh có prefix * là đang xét

git branch -r // xem nhánh các nhánh từ các remote repo

git branch -a // liệt kê tất cả nhánh local và remote
```
For example, giờ mình muốn tạo thêm một hàm chức năng vào file `example.c` của mình, giả sử, tính năng cộng 2 số a và b cho trước, giờ ta sẽ tạo một nhánh mới có tên là `add-sum`, sau đó dùng lệnh `git branch` để kiểm tra sự tồn tại của các nhánh.
```
$ git branch
  add-sum
* master
```
Như bạn thấy, giờ đây đang tồn tại 2 nhánh là nhánh chính **master** và nhánh mình mới tạo **add-sum**. Dấu * cho thấy vị trí làm việc của mình đang ở nhánh master.

---
## Chuyển nhánh làm việc
Ta dùng `git checkout` để chuyển nhánh làm việc của mình. 
```
git checkout <branch_name> //Switch tới nhánh branch_name

git checkout -b <branch_name>

```
Áp dụng tham số -b sẽ tạo một nhánh mới và chuyển ngay đến nhánh đó (kết hợp giữa 2 lệnh `git branch <branch_name> && git checkout <branch_name>`)

Thử chuyển nhánh đến nhánh `add-sum`, ta có:
```
$ git checkout add-sum 
Switched to branch 'add-sum'
```
Muốn xóa một nhánh dùng lệnh
```
git branch -d <name-branch>
```
Trong file `example.c` sửa như sau:
```
#include <stdio.h>

int add(int a, int b) {
    return a+b;

}
int main() {
    int a;
    printf("Hello World");
    return 0;
}
```
Ta thêm hàm add vào (đây là ví dụ đơn giản trong thực tế, nhánh sẽ phát huy tác dụng khi ta chia công việc phát triển các tính năng cho nhiều người).

Nếu ta dùng lệnh `branch` để chuyển nhánh sang nhánh master, ta soi file `example.c`, ta sẽ không thấy hàm `add`. Vì nhánh `add-sum` đang tồn tại song song và chưa kết hợp với nhánh chính.

Giờ dùng lệnh add để đưa file .c vào trạng thái stage và dùng commit để commit file .c:
```
$ git status
On branch add-sum
Changes to be committed:
  (use "git restore --staged <file>..." to unstage)
        new file:   example.c

$ git commit -m "Add sum feature to the main function" 
[add-sum 5599270] Add sum feature to the main function
 1 file changed, 11 insertions(+)
 create mode 100644 example.c

```
Giờ đến bước merge (trộn) nó với nhánh chính master.

---
## Trộn nhánh (Merge)
Sau khi mình đã phát triển tính năng hoặc fix một lỗi nào xong, đến lúc merge nó vào chương trình chính.
For example, để merge nhánh *add-sum* vào nhánh master để thu được tính năng `add`, từ nhánh `add-sum` ta phải checkout về nhánh chính `master`, sau đó dùng lệnh `git merge`:

```
$ git checkout master
$ git merge add-sum 
Updating aa9eeae..5599270
Fast-forward
 example.c | 11 +++++++++++
 1 file changed, 11 insertions(+)
 create mode 100644 example.c
```
Giờ kiểm tra file `example.c` thì đã có hàm *add*.

---
# Github
Git chỉ là môi trường quản lí code trên máy mình, muốn chia sẻ code để mọi người cùng làm việc thì phải up lên Github.

Lên Github tạo tài khoản, tạo repository rồi code link repo đó, giả sử mình tạo một repo *documents*, được link như này:
```
https://github.com/4utumnRain/documents
```
Giờ ta muốn up code từ máy mình lên github.

---
## Git remote

Liệt kê tất cả các remote của các repo mà bạn đang có.
```
git remote 
hoặc 
git remote -v (nếu muốn xem dưới dạng đường link url) 
```


Tạo 1 kết nối mới đến link url
```
git remote add <name> <url>
```
Example, mình gõ thì:
```
$ git remote add origin https://github.com/4utumnRain/documents 

trong đó `origin` là 1 shortcut cho `url` mà 
mình hướng đến, ở đây hướng đến repo documents của mình. 



$ git remote
origin

$ git remote -v
origin  https://github.com/4utumnRain/documents (fetch)
origin  https://github.com/4utumnRain/documents (push)

```
Bỏ kết nối tới repo `name` bằng lệnh
```
git remote rm <name>
```
Đổi tên quy ước `name` bằng lệnh:
```
git remote rename <old-name> <new-name>
```
For example, mình đổi tên hiện tại `origin` thành `main`:
```
$ git remote rename origin main
Renaming remote references: 100% (5/5), done.
$ git remote
main
```

## Đẩy code lên github
Example, dùng `git push`:
```
$ git push --set-upstream main master
Enumerating objects: 9, done.
Counting objects: 100% (9/9), done.
Delta compression using up to 8 threads
Compressing objects: 100% (7/7), done.
Writing objects: 100% (7/7), 1.96 KiB | 1002.00 KiB/s, done.
Total 7 (delta 2), reused 0 (delta 0), pack-reused 0
remote: Resolving deltas: 100% (2/2), completed with 1 local object.
To https://github.com/4utumnRain/documents
   ff6c3a2..5599270  master -> master
branch 'master' set up to track 'main/master'.
```
check lại github thì thấy các file của mình đã được up lên github.
<!-- 
```
git remote show <name>
```
Hiện 1 list nhánh liên quan đến remote `name` đó và các điểm cuối để fetch and push -->

Setpoint ở đây



## Git fetch 
Cập nhập những update về local repository
```
git fetch <github-branch> 
```
for example, 
```
git fetch main/master

or 

git fetch   #để kéo hết các nhánh về
```
lệnh trên kéo những update từ nhánh main/master của mình trên github về.

## Git merge
Dùng để trộn những thay đổi của repo trên github vào repo mình
```
git merge main/master
```
lệnh trên sẽ trộn tất cả những update trên nhánh main/master trên github của mình về branch hiện tại.

## Git pull 
Lệnh kết hợp của fetch và merge.
```
git pull main/master

or 

git pull  %để kéo hết các nhánh 
```

## Git push to github 
Sau khi commit những thay đổi trong file trong repo của bạn, ta thử kiểm tra những update bằng lệnh `status`:
```
$ git status
On branch master
Your branch is ahead of 'main/master' by 1 commit.
  (use "git push" to publish your local commits)

nothing to commit, working tree clean

```
ta thấy ta đang trước nhánh trên github 1 commit, để đẩy lên tiến hành thực hiện lệnh `push`:
```
$ git push main
Enumerating objects: 5, done.
Counting objects: 100% (5/5), done.
Delta compression using up to 8 threads
Compressing objects: 100% (3/3), done.
Writing objects: 100% (3/3), 5.12 KiB | 2.56 MiB/s, done.
Total 3 (delta 1), reused 0 (delta 0), pack-reused 0
remote: Resolving deltas: 100% (1/1), completed with 1 local object.
To https://github.com/4utumnRain/documents
   7ca6ee3..38594d6  master -> master
```
có thể lên github để kiểm tra những thay đổi.

## Git clone
Git clone sẽ tạo 1 kết nối remote ở repo mà bạn clone về.


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