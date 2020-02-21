## MariaDB 설치 및 환경 설정

- MariaDB 설치 확인

  ~~~bash
  rpm -qa | grep mariadb
  ~~~

- MariaDB 삭제

  ~~~bash
  sudo yum remove mariadb-*
  ~~~

- MariaDB 설치

  ~~~bash
  sudo yum install mariadb-*
  ~~~

- 서버 재기동 시 자동 실행

  ~~~bash
  sudo systemctl enable mariadb
  ~~~

- Character Set 설정 

  character set은 "utf8"은 최초 mysql 설계시 utf8 규격에 4byte에 할당된 문자가 없어 3byte로 설계되었으나 최근 4byte에 할당된 문자(**이모티콘 문자**)가 생기면서 4byte 확장을 위해 utf8mb4를 추가하였다. **utf8** 규격과 동일한 **utf8mb4**로 설정할 것을 권장하고 있다.

  ~~~bash
  sudo vi /etc/my.cnf.d/server.cnf
  
  [mysqld]
  character-set-server=utf8mb4
  collation-server=utf8mb4_bin
  lower_case_table_names=1 #테이블명 대소문자 구분 해제
  ~~~

  ~~~bash
  sudo vi /etc/my.cnf.d/mysql-clients.cnf
  
  [mysql]
  default-character-set=utf8mb4
  [mysqldump]
  default-character-set=utf8mb4
  ~~~

- mysql 실행 (초기 비밀번호 없음)

  ~~~bash
  mysql -u root
  ~~~
  
- root 비밀번호 설정

  ~~~mysql
  use mysql
  update user set password=password('변경 할 비밀번호') where user='root';
  flush privileges;
  ~~~

- 테이블 character_set 확인

  ~~~mysql
  show variables like 'c%';
  ~~~

- 데이터베이스 생성

  ~~~mysql
  create database selvy_ocr_server;
  ~~~

- 사용자 생성 및 권한 부여

  ~~~mysql
  # 외부(원격) 접속
  create user 'admin'@'%' identified by 'abcd123$';
  # 로컬 접속
  create user 'admin'@'localhost' identified by 'abcd123$';
  grant all privileges on selvy_ocr_server.* to admin@'%';
  flush privileges;
  ~~~

