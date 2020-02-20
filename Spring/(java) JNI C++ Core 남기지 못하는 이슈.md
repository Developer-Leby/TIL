##  JNI C++ Core 남기지 못하는 이슈

Java에서 JNI로 C++ 엔진 호출 시 C++에서 Crush 발생할 때 Core가 생성 되는데, Core가생성되지 않고 다음과 같이 문구가 나오는 경우

~~~bash
Failed to write core dump. Core dumps have been disabled. To enable core dumping, try "ulimit -c unlimited" before starting Java again
~~~

다음과 같이 명령어를 사용하면 정상적으로 Core 파일이 생성 된다.

~~~bash
ulimit -c unlimited # Core 메모리 상관없이 생성

ulimit -c -l # unlimited로 설정되어 있는지 확인
core file size          (blocks, -c) unlimited
max locked memory       (kbytes, -l) 64
~~~

