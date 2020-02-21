## 데이터 Export (.csv)

~~~mysql
SELECT * FROM TB_DOCUMENT
INTO OUTFILE '/app/share/server1_tb_document.csv'
CHARACTER SET utf8
FIELDS TERMINATED BY ';'
ENCLOSED BY '\"'
LINES TERMINATED BY '\n'
~~~

>1 (HY000): Can't create/write to file '/app/share/server1.csv' (Errcode: 13)
>
>위와 같은 에러는 mysql의 권한 문제이다. 방법은 다음과 같다.
>
>1. 디렉터리의 권한을 chmod 777로 모두 사용 가능하도록 변경한다. (비추천)
>2. mysql의 디렉터리를 위치를 변경한다. (추천)

~~~mysql
SELECT * FROM TB_DOCUMENT
INTO OUTFILE '/var/lib/mysql/server1_tb_document.csv'
CHARACTER SET utf8
FIELDS TERMINATED BY ';'
ENCLOSED BY '\"'
LINES TERMINATED BY '\n'
~~~



## 데이터 Import (.csv)

~~~mysql
LOAD DATA LOCAL INFILE '/var/lib/mysql/server1_tb_document.csv'
INTO TABLE selvy_ocr_server.TB_DOCUMENT
FIELDS TERMINATED BY ';'
ENCLOSED BY '\"'
LINES TERMINATED BY '\n'
~~~

