## Hướng dẫn sử dụng GIT cho người mới bắt đầu

**1. Git là gì? Tại sao phải sử dụng GIT?**

https://backlog.com/git-tutorial/vn/intro/intro1_1.html

**2. Cài đặt và cấu hình GIT**

- Cài đặt Git Bash [ở đây](https://git-scm.com/download/win)
- Cấu hình GIT: `name/email` cho commit

    - Thiết lập cho tất cả repository
        ```
        $ git config --global user.name "Example Kiaisoft"
        $ git config --global user.email "example@kiaisoft.com"
        ```
    - Thiết lập cho repository
        ```
        $ git config user.name "Example Kiaisoft"
        $ git config user.email "example@kiaisoft.com"
        ```

**3. Các lệnh cơ bản của GIT:**

- Lệnh `git clone`: Kéo source code từ remote repository về local 
    ```
    $ git clone git@gitlab.kiaisoft.com:training/document.git
    ```
- Lệnh `git add` files: Đẩy các files tới staging area
    ```
    $ git add /path/file1.md /path/file2.md
    ```
- Lệnh `git commit`: Đẩy commit lên local repository
    ```
    $ git commit -m "Login Function is done"
    ```
- Lệnh `git push`: Đẩy commit lên remote repository
    ```
    $ git push"
    ```
- Lệnh `git pull`: Kéo commit từ remote repository về local

    - Kéo code về cùng một nhánh `master`
        ```
        $ git pull origin master
        ```
    - Kéo code ở nhánh `develop` về `master`
        ```
        $ git pull origin develop
        ```
- Lệnh `git status` check trạng thái của file
    ```
    $ git status
    ```
- Lệnh `git log` xem lịch sử `commit`
    ```
    $ git log
    $ git log --pretty=format:"%h - %an, %ar : %s"
    $ git log --pretty=format:"%h %s" --graph
    ```
- Lệnh `git diff` Để xem trạng thái thay đổi của file nhưng chưa được `staged`
    ```
    $ git diff 
    ```   
- Lệnh `git checkout` Hoàn nguyên lại file đã bị thay đổi trong `working tree`
    ```
    $ git checkout /path/file1.md
    ```  
- Lệnh `git fetch` Kéo các thay đổi ở remote repository về local repository
    ```
    $ git fetch
    ```  

**4. Làm việc với nhánh trong GIT**

- Tạo nhánh `develop` từ nhánh base `master`
    ```
    $ git checkout -b develop
    ```
- Chuyển đổi giữa các nhánh
    ```
    $ git checkout master
    ```
- Merge nhánh `develop` tới nhánh `master`
    ```
    $ git merge develop
    ```    
- Xóa nhánh `develop`
    ```
    $ git branch -d develop
    ``` 
    
**5. Ignoring Files**

- Nếu không muốn `GIT` theo dõi các file/folder không cần thiết thì có thể dụng file `.gitignore` để khai báo.
Mỗi lần `add` hay `commit` GIT sẽ bỏ qua các file/folder mà không đẩy chúng vào repository.  
- Tạo file `.gitignore` trong thư mục repository.
- Thêm các file hoặc thư mục ko muốn commit lên git, ví dụ:
    ```git
     /public/storage/*
     /vendor
     # ignore all .env files
     *.env
     # but do track develop.env, even though you're ignoring .env files above
     !develop.env
     .idea/workspace.xml
     # ignore all .pdf files in the doc/ directory and any of its subdirectories
     doc/**/*.pdf
    ```
**6. Các lệnh GIT nâng cao**
- Liệt kê các thiết lập đang sử dụng
    ```
    $ git config --list
    ```
- Liệt kê & thay đổi origin url
    ```
    $ git remote -v
    $ git remote set-url origin git@gitlab.kiaisoft.com:training/document-other.git
    ```
- Sử dụng lệnh `git stash` để lưu các thay đổi chưa `commit`
    ```
    # Lưu các thay đổi
    $ git stash save 
    
    # Lấy lại thay đổi
    $ git stash list
        stash@{0}: WIP on <branch-name>: <lastest commit>
        stash@{1}: WIP on <branch-name>: <lastest commit>
        stash@{2}: WIP on <branch-name>: <lastest commit>
    $ git stash apply stash@{0}
    
    # Xoá các thay đổi không cần thiết
    $ git stash drop stash@{1}
    
    # Xóa toàn bộ stack
    $ git stash clear
    ```
- Xem thay đổi giữa hai commits
    ```
    $ git diff COMMIT1_ID COMMIT2_ID
    ```
- Revert một commit rồi push
    ```
    $ git revert COMMIT_ID
    $ git push origin master
    ```
- Revert đến thời điểm trước một commit
    ```
    $ git reset COMMIT_ID
    $ git reset --soft HEAD@{1}
    $ git commit -m "Revert to COMMIT_ID"
    $ git reset --hard
    ```    
- Undo commit gần nhất, vẫn giữ thay đổi ở local
    ```
    $ git reset --soft HEAD~1
    ```
- Undo commits chưa push
    ```
    $ git reset origin/master
    ```
- Reset về trạng thái của remote
    ```
    $ git fetch origin
    $ git reset --hard origin/master
    ```
- Xoá toàn bộ các files chưa đc track
    ```
    $ git clean -f
    $ git clean -f -d
    ```
- Sử dụng `git cherry-pick` nhặt commit `99daed2` từ branch này tới branch `master`
    ```
    $ git checkout master
    $ git cherry-pick 99daed2
    ```
- Khi muốn đổi tên user hoặc email của HEAD
     ```
     $ git commit --amend -m "commit message" --author="Example <example@kiaisoft.com>"
     ```
- Trường hợp muốn sửa lại commit bất kì
    ```
    $ git rebase -i <commit>
    
    ====
    # Sau lệnh này sẽ mở ra editor nên hãy sửa lại như sau rồi lưu lại
    
    # (trước khi sửa) các commit cũ từ trên xuống dưới
    pick aa11bbc commit message 1
    pick b2c3c4d commit message 2
    pick 4e56fgh commit message 3
    ・・・
    
    # (Sau khi sửa) Đổi commit cần sửa sang edit
    edit aa11bbc commit message 1
    pick b2c3c4d commit message 2
    pick 4e56fgh commit message 3
    ・・・
    ====
    
    # Sau đó thì sửa tương tự
    $ git commit --amend -m "commit message" --author="user.name <user.email>"
    
    # Trở lại như cũ
    $ git rebase --continue
    ```
 - Trường hợp muốn gộp một số commit trước đó (tính từ commit latest)
    ```
    $ git rebase -i head~3     (rebase 3 commit gần đây nhất)
    
    ====
    
    # (trước khi sửa) các commit cũ từ trên xuống dưới (commit 3 là gần đây nhất)
    pick aa11bbc commit message 1
    pick b2c3c4d commit message 2
    pick 4e56fgh commit message 3
    ・・・
    
    # (Sau khi sửa) Đổi commit cần gộp thành 'pick' -> 'squash' hoặc viết tắt là 's'
    pick aa11bbc commit message 1
    squash(s) b2c3c4d commit message 2
    squash(s) 4e56fgh commit message 3
    ・・・
    ====
    
    # Sau đó thì sửa tương tự
    $ git commit --amend -m "combine commit"
    
    # Trở lại như cũ
    $ git push origigin -f head 
    ```
**7. Cách sử dụng gitlab của công ty**

- Tạo một cặp public/private key và thêm vào gitlab
https://gitlab.kiaisoft.com/profile/keys
    ```
    $ ssh-keygen
    ```
- Tạo file `config` cho ssh. Di chuyển đến thư mục `~/.ssh`, thêm file `config` với nội dung.
    ```
    Host gitlab.kiaisoft.com
        Port 2200
        User git
        IdentityFile ~/.ssh/id_rsa
    ```

    

**10. Tham khảo**

- https://git-scm.com/book/en/v2

- https://backlog.com/git-tutorial/vn/intro/intro1_1.html

- https://viblo.asia/p/19-bi-kip-ban-co-the-dung-khi-pham-sai-lam-voi-git-dWrvwdmPRw38










# Project Coding Convention

- Quy tắc đặt tên:
	- Controller: 
		- Đặt tên controller tường minh dễ hiểu, không quá dài (max 3 từ)
		- Ví dụ với chức năng graph setting thì đặt tên là GraphSettingController thay vì SettingController(chung chung, không biết Setting cho cái gì)
		- Không dùng Model trực tiếp trong Controller mà gọi từ Repository
		- Hạn chế dùng raw query mà sử dụng Eloquent, trừ trường hợp Query quá phức tạp(ví dụ join nhiều bảng, lấy dữ liệu xử lí phức tạp...)
	- Request: 
		- Đặt tên Request không quá dài (max 3 từ), kết thúc bằng Request 
		- Ví dụ (CreateUserRequest)
		- Sử dụng rules và attributes (rules để quy định cách validate, attributes quy định tên của đối tượng validate)
		- Sử dụng custom validation nếu rules và attributes ko handle hết được
		- Sử dụng Rule của laravel nếu cần validate phức tạp. Document [https://laravel.com/docs/6.x/validation#using-rule-objects](https://laravel.com/docs/6.x/validation#using-rule-objects "https://laravel.com/docs/6.x/validation#using-rule-objects")
		- Nếu có những message đặc biệt mà trong request ko xử lý được bằng attritube thì nên viết vào đoạn Custom Validation Language Lines của file validation.jp
	- Về Route: 
		- Với các chức năng CRUD, tận dụng hết các route theo restful, tên dễ hiểu, tường minh, có namespace
		- Viết theo chuẩn kebab-case (cách từ bằng dấu -) 
		- Ví dụ: 
			- Không nên viết: createGraphSetting, list_graph_setting ......
			- Nên viết: graph-settings.index, graph-settings.create (tên resource - tên action)
	
	- Về cách đặt tên biến:
		- Có thể sử dụng camelCase($colorCodes) hoặc snake_case ($color_codes), tuy nhiên nên dùng camelCase
	
	- Về view
		- Đặt tên theo chuẩn kebab-case
		- Ví dụ: Không nên đặt tên là settingAccount.blade.php => nên viết là setting-account.blade.php
		- Các màn hình con trong một chức năng đặt trong cùng 1 folder (tên folder cũng viết theo kebab-case)
	
- Quy tắc coding
	- Luôn phải check isset khi gọi thuộc tính của 1 object có thể là null
		- Đặc biệt khi lấy thuộc tính của 1 relationship (ví dụ user->profile->user_name)
		- Trong trường hợp này phải check user->profile có null không trước khi gọi đến property user_name 
		=> phải check isset của thằng cha trước, hoặc dùng php 7 null coalescing operator (google)
		- isset(user->profile)
		- optional(user->profile)->user_name
		- user->profile->user_name ?? ''
		
	- Không hard-coding , với các magic number thì phải define ở file constant
	- Với các function sử dụng nhiều thì viết vào Helper
	

- Quy tắc khi code front end
	- Button: Phải đồng nhất màu và vị trí đặt btn. Như ví dự bên dưới
		- Save, search, preview, add new, send message: màu xanh lá
		- Cancel: màu gray
		- Delete: màu đỏ
	- Các field required: phải có dấu * đỏ ở label. Validate dòng chữ màu đỏ để ở dưới ô input sử dụng thẻ span và class span. Tham khảo ở template adminlte
	- Trong form label và input đều căn trái
	- Code ở file blade phải tách riêng các phân css, content, js. Css => section('style'), JS => section('script'), content => section('content')


**Lưu ý: Mọi người nên tham khảo template trước khi code**
