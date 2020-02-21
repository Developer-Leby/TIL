# crontab

리눅스에서 배치 형태의 작업을 진행해야 할 때 사용되는 프로세스 (특정 시간에 특정 작업을 해야한다.)

윈도우의 스케줄러와 비슷한 역할을 한다고 보면 된다.

- **crontab 등록**

  ~~~bash
  crontab -e
  
  # 1분마다 메모리 60% 체크 확인 서버 재기동
  * * * * * /app/bin/memory_check.sh
  ~~~

  crontab 문법 규격에 맞게 작성하고 wq로 종료하면 crontab이 갱신됩니다.

- **crontab 확인**

  ~~~bash
  crontab -l
  
  # 1분마다 메모리 60% 체크 확인 서버 재기동
  * * * * * /app/bin/memory_check.sh
  ~~~

- **crontab 주기 설명**

  ~~~bash
     *          *          *         *         *
  분(0-59)　　시간(0-23)　　일(1-31)　　월(1-12)　　요일(0-7)
  ~~~

  

