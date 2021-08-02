---
layout: custom-single
title:  "백업 및 복원"
categories:
  - mariadb
tags: [programming, database, mariadb]

author_profile: true
sidebar:
  nav: "docs"

toc: true
toc_label: "목록"
toc_icon: "bars"
toc_sticky: true

comments: true

date: 2021-08-02
---

#### MariaDB 백업
---

데이터베이스별로 백업파일을 만든다.
```sh
mysqldump [options] -u[user] -p[password] > [backupfile_path]
```

employee라는 데이터베이스를 백업하는 예제이다.
```sh
mysqldump --single-transaction --routines --triggers --databases employee -uroot -p1234 > ~/backup/employee_20210802_0200.sql
```

전체 데이터베이스를 백업한다.
```sh
mysqldump --single-transaction --routines --triggers --all-databases -uroot -p1234 > ~/backup/all_20210802_0200.sql
```

### MariaDB 복원
---

위의 예제에서 백업된 데이터베이스를 기준으로 예제를 작성한다.
하나의 데이터베이스를 복원할 때 해당 데이터베이스가 없다면 생성한다.
```sh
mysqladmin -uroot -p1234 create employee
```

데이터베이스를 복원한다.  
만약 프로시져등에 주석이 있다면 --comments옵션을 넣어서 주석도 같이 복원하도록 한다.
```sh
mysql -uroot -p1234 --comments employee < ~/backup/employee_20210802_0200.sql
```

전체 데이터베이스를 복원한다.
```sh
mysql -uroot -p1234 --comments < ~/backup/all_20210802_0200.sql
```