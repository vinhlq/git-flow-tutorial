# Index

1. [Introduction](#introduction)
2. [Installation](#installation)
3. [Workflow](#workflow)
4. [Vai trò của các nhánh](#branching)
5. [Developer workflow](#developer-work-flow)
6. [Maintainer workflow](#maintainer-work-flow)
7. [Tham khảo](#references)

# <a name="introduction"></a>Introduction

- [Git flow](https://github.com/nvie/gitflow) là một cơ chế quản lý [semantic](https://semver.org) version cho git project
- Tài liệu này nhằm làm rõ vai trò của developer và maintainer trong git-flow

# <a name="installation"></a>Installation
1. [Linux](https://github.com/nvie/gitflow/wiki/Linux)
    - Debian & Ubuntu
        > apt install git-flow
2. [Windows](https://github.com/nvie/gitflow/wiki/Windows)

# <a name="workflow"></a>Workflow
1. Maintainer(M) khởi tạo project và push lên remote git
2. Developer(D) clone project từ remote git
3. D bắt đầu phát triển 1 tính năng(feature)
4. D publish feature lên remote git
5. D bắt đầu 1 bug-fix
6. D publish bug-fix lên remote git
7. D bắt đầu 1 hot-fix
8. D publish hot-fix lên remote git
9. M update 1 feature từ remote git
10. M update 1 bug-fix từ remote git
11. M merge các features và bug-fix
12. M release 1 stable version
13. M update 1 hot-fix từ remote git
14. M release 1 hot-fix version

# <a name="branching"></a>Vai trò của các nhánh
1. Master:
    - Là nhánh chỉ chứa các stable release version
    - Tồn tại cả ở remote và local git
2. Develop
    - Là nhánh phát sinh tạm thời phục vụ cho quá trình develop
    - Là mirror của master HEAD version
    - Chỉ tồn tại ở local
3. Feature/feature_name & bugfix/bugfix_name
    - Là nhánh phát sinh tạm thời phục vụ cho quá trình develop
    - Là mirror của develop HEAD
    - Tồn tại ở remote và local git
    - Có thể xóa khi kết thúc quá trinh
4. Release/version_name
    - Là nhánh phát sinh tạm thời phục vụ cho quá trình release
    - Là mirror cả develop HEAD
    - Chỉ tồn tại ở local
    - Xóa khi kết thúc quá trinh
5. Hotfix/version
    - Là nhánh phát sinh tạm thời phục vụ cho quá trình fix bug tồn tại trên master
    - Là mirror của master base version
    - Chỉ tồn tại ở local
    - Xóa khi kết thúc quá trinh

# <a name="developer-work-flow"></a>Developer workflow
## Vai trò của developer
1. Phát triển các tính năng(feature)
2. Fix bug
3. Phát hành version hotfix
## Các bước thực hiện
1. Clone project từ remote git
2. Init git-flow
    > git flow init
    
    Sau bước này sẽ tạo ra 1 nhánh develop mirror từ nhánh master
    
3. Thêm 1 feature cho project (feature)
- Start
    > git flow feature start feature_name

    Sau bước này sẽ tạo ra 1 nhánh feature/feature_name mirror từ nhánh develop

- Publish feature lên remote git
    > git flow feature publish feature_name

    Sau bước này trên remote git sẽ có thêm nhánh feature/feature_name là mirror của local

- Cập nhật 1 tính năng từ remote git
    > git flow feature track feature_name

    Sau bước này local git sẽ có thêm nhánh feature/feature_name là mirror của remote

4. Fix-bug
    - Start
        > git flow bugfix start bugfix_name

        Sau bước này sẽ tạo ra 1 nhánh bugfix/bugfix_name mirror từ nhánh develop

    - Publish nhánh bug-fix lên remote git
        > git flow bugfix publish bugfix_name

        Sau bước này trên remote git sẽ có thêm nhánh bugfix/bugfix_name là mirror của local

    - Cập nhật nhánh bug-fix từ remote git
        > git flow bugfix track bugfix_name

        Sau bước này local git sẽ có thêm nhánh bugfix/bugfix_name là mirror của remote

5. Hot-fix
    - Start
        > git flow hotfix start VERSION [BASE_VERSION]

        Bắt đầu sửa lỗi cho version BASE_VERSION, **VD base version là 1.0 hotfix version là 1.0.1**
        Sau bước này sẽ tạo ra 1 nhánh hotfix/VERSION mirror từ nhánh master

    - Publish nhánh hot-fix lên remote git
        > git flow hotfix publish VERSION

        Sau bước này trên remote git sẽ có thêm nhánh hotfix/VERSION là mirror của local

    - Cập nhật nhánh bug-fix từ remote git
        > git flow hotfix track VERSION

        Sau bước này local git sẽ có thêm nhánh hotfix/VERSION là mirror của remote

# <a name="maintainer-work-flow"></a>Maintainer workflow
## Vai trò của maintainer:
1. Kết thúc quá trình phát triển thêm feature và bug-fix
2. Release version từ nhánh develop về master
## Các bước thực hiện
1. Clone project từ remote git
2. Init git-flow
    > git flow init
    
    Sau bước này sẽ tạo ra 1 nhánh develop mirror từ nhánh master
    
3. Merge 1 feature từ remote git
    - Update
        > git flow feature track feature_name
        
        Sau bước này local git sẽ có thêm nhánh feature/feature_name là mirror của remote
        
    - Merge
        > git flow feature finish feature_name
        
4. Merge 1 bug-fix từ remote git
    - Update
        > git flow bugfix track bugfix_name
        
        Sau bước này local git sẽ có thêm nhánh bugfix/bugfix_name là mirror của remote
        
    - Merge
        > git flow bugfix finish bugfix_name
        
5. Release version từ nhánh master
    - Start
        > git flow release start VERSION [BASE_VERSION]
    - Finish
        > git flow release finish VERSION
    - Push
        > git push origin master
        > git push --follow-tags origin
6. Release hot-fix
    - Update
        > git flow hotfix track VERSION
        
        Sau bước này local git sẽ có thêm nhánh hotfix/VERSION là mirror của remote
    - Finish
        > git flow hotfix finish VERSION
    - Push
        > git push origin master
        > git push --follow-tags origin
        

# <a name="references"></a>Tham khảo
1. [Git-flow workflow](https://www.atlassian.com/git/tutorials/comparing-workflows/gitflow-workflow)
2. [Git-flow cheatsheet](https://danielkummer.github.io/git-flow-cheatsheet)
3. [The easy release management workflow](https://blog.axosoft.com/gitflow)
