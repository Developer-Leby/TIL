## 서버 이중화 MySQL 인스턴스 공유

- **서버 이중화 하기 위해 MariaDB 인스턴스 디렉터리를 1번 서버와 2번 서버가 함께 공유하도록 설정**

~~~bash
MariaDB 디렉터리 경로를 공유 디렉터리 경로로 설정하여 인스턴스 시작했더니 오류
~~~

- **해결 방법**

~~~bash
Replication 사용하여 데이터베이스 이중화 설정 (데이터베이스를 동기화 하는 방식)
Master / Slave 형태로 구성 => 양방향 구성 가능 1번 (Master/Slave), 2번 (Master/Slave)
~~~

