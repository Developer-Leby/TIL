##GDB 환경 설정 및 테스트

- gdb 설치 확인

  ~~~bash
  rpm -qa | grep gdb
  ~~~

- gdb 설치

  ~~~bash
  sudo yum -y install gdb
  ~~~

- 어떤 프로세스의 core dump인지 확인

  ~~~bash
  file core.6157
  
  core.6157: ELF 64-bit LSB core file x86-64, version 1 (SYSV), SVR4-style, from 'java -Xmx1024m -Xms512m -Dserver-environment.server-index=-1 -Dserver-environme', real uid: 0, effective uid: 0, real gid: 0, effective gid: 0, execfn: '/usr/bin/java', platform: 'x86_64'
  ~~~

- core dump 분석

  ~~~bash
  gdb /usr/bin/java core.6157
  
  (gdb) bt 
  #0  0x00007fcf4e1e6277 in raise () from /lib64/libc.so.6
  #1  0x00007fcf4e1e7968 in abort () from /lib64/libc.so.6
  #2  0x00007fcf4da84f69 in os::abort(bool) () from /usr/lib/jvm/java-1.8.0-openjdk-1.8.0.232.b09-0.el7_7.x86_64/jre/lib/amd64/server/libjvm.so
  #3  0x00007fcf4dc8f136 in VMError::report_and_die() () from /usr/lib/jvm/java-1.8.0-openjdk-1.8.0.232.b09-0.el7_7.x86_64/jre/lib/amd64/server/libjvm.so
  #4  0x00007fcf4da8efb5 in JVM_handle_linux_signal () from /usr/lib/jvm/java-1.8.0-openjdk-1.8.0.232.b09-0.el7_7.x86_64/jre/lib/amd64/server/libjvm.so
  #5  0x00007fcf4da82128 in signalHandler(int, siginfo_t*, void*) () from /usr/lib/jvm/java-1.8.0-openjdk-1.8.0.232.b09-0.el7_7.x86_64/jre/lib/amd64/server/libjvm.so
  #6  <signal handler called>
  #7  0x00007fcef85e6b12 in DocRecognizer::recognizer(std::string, std::string, std::string) () from /app/share/bin/liblotte_e_commerce.so
  #8  0x00007fcef88b1268 in recognizer::nRecognize(JNIEnv_*, _jobject*, long, _jstring*, _jstring*, _jstring*) () from /app/share/bin/libjni_selvy_ocr.so
  #9  0x00007fcf38e11f27 in ?? ()
  #10 0x0000000000000000 in ?? ()
  ~~~