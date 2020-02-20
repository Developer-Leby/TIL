## Replication 이중화 설정

**1번 서버  `MASTER 설정 `**

- server.conf 설정

  ~~~bash
  vi /etc/my.cnf.d/server.cnf
  
  [mariadb]
  log-bin
  server_id=1
  log-basename=master1
  ~~~

- MariaDB 재시작

  ~~~bash
  sudo systemctl stop mariadb
  sudo systemctl status mariadb
  sudo systemctl start mariadb
  ~~~

- MariaDB 접속

  ~~~bash
  mysql -u root
  ~~~

- Replication 아이디 생성 및 권한 설정

  ~~~mysql
  CREATE USER 'leby'@'%' IDENTIFIED BY 'test1234!';
  GRANT REPLICATION SLAVE ON *.* TO ocr;
  ~~~

- Master 정보 확인

  ~~~mysql
  show master status;
  
  +--------------------+----------+--------------+------------------+
  | File               | Position | Binlog_Do_DB | Binlog_Ignore_DB |
  +--------------------+----------+--------------+------------------+
  | master1-bin.000001 |      464 |              |                  |
  +--------------------+----------+--------------+------------------+
  ~~~

<br/>

**2번 서버 `Slave 설정`**

- server.conf 설정

  ~~~bash
  vi /etc/my.cnf.d/server.cnf
  
  [mariadb]
  server-id=11
  log-bin
  log-basename=master1
  report-host=slave1
  expire_logs_days = 30
  max_binlog-size = 100M
  ~~~

- MariaDB 재시작

  ~~~bash
  sudo systemctl stop mariadb
  sudo systemctl status mariadb
  sudo systemctl start mariadb
  ~~~

- MariaDB 접속

  ~~~bash
  mysql -u root
  ~~~

- Slave 아이디 정보 확인

  ~~~mysql
  show variables like 'server_id';
  
  +---------------+-------+
  | Variable_name | Value |
  +---------------+-------+
  | server_id     | 11    |
  +---------------+-------+
  ~~~

- Slave - Master 설정

  ~~~bash
  CHANGE MASTER TO
      -> MASTER_HOST='1번 서버 IP',
      -> MASTER_USER='leby',
      -> MASTER_PASSWORD='test1234!',
      -> MASTER_PORT=3306,
      -> MASTER_LOG_FILE='master1-bin.000001',
      -> MASTER_LOG_POS=464,
      -> MASTER_CONNECT_RETRY=10;
  ~~~

- Slave Replication 시작

  ~~~mysql
  START SLAVE;
  ~~~



## 양방향 Replication 설정

- 2번 서버가 Master가 되고 1번 서버가 Slave가 되는 설정으로 동일하게 구성하면 된다.

