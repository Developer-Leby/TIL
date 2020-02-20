## JNI C++ 연동 간 발생 이슈 (OCR Engine)

- **아래 로그와 함께 서버 중지**

~~~bash
global_init::start
2020-01-07 11:23:35.056367: I tensorflow/core/platform/profile_utils/cpu_utils.cc:94] CPU Frequency: 2194710000 Hz
2020-01-07 11:23:35.058125: I tensorflow/compiler/xla/service/service.cc:168] XLA service 0x7fa9f0e4ca20 initialized for platform Host (this does not guarantee that XLA will be used). Devices:
2020-01-07 11:23:35.058214: I tensorflow/compiler/xla/service/service.cc:176]   StreamExecutor device (0): Host, Default Version
global_init::end run time: 1579.029500
recognizer::start
test_net::start
java: /pytorch/third_party/ideep/mkl-dnn/src/common/memory_tracking.hpp:240: void* mkldnn::impl::memory_tracking::registry_t::get(const key_t&, void*) const: assertion `size() == 0' 실패.
중지됨
~~~

>**문제 해결** 
>
>메모리가 부족 로그 확인
>
>서버 메모리 4GB => 8GB 업그레이드하니 정상 동작

<br/>

<br/>

- **jni java.library.path 못 찾는 현상**

  Linux 환경에서 .bash_profile에 LD_LIBRARY_PATH so 파일 경로 설정을 하였는데도 계속 발생

~~~bash
java.lang.UnsatisfiedLinkError: no jni_selvy_ocr in java.library.path
        at java.lang.ClassLoader.loadLibrary(ClassLoader.java:1867)
        at java.lang.Runtime.loadLibrary0(Runtime.java:870)
        at java.lang.System.loadLibrary(System.java:1122)
        at com.selvasai.selvyocr.recognizer.PyRecognizer.loadLibrary(PyRecognizer.java:32)
        at com.selvasai.selvyocr.recognizer.PyRecognizer.<init>(PyRecognizer.java:12)
        at com.selvasai.selvyocr.recognizer.PyRecognizer.getInstance(PyRecognizer.java:19)
        at com.selvas.ocrserver.job.OcrEngineJob.execute(OcrEngineJob.java:55)
        at org.quartz.core.JobRunShell.run(JobRunShell.java:202)
        at org.quartz.simpl.SimpleThreadPool$WorkerThread.run(SimpleThreadPool.java:573)
Exception in thread "pool-3-thread-1" java.lang.UnsatisfiedLinkError: com.selvasai.selvyocr.recognizer.PyRecognizer.nInitialize(Ljava/lang/String;)I
        at com.selvasai.selvyocr.recognizer.PyRecognizer.nInitialize(Native Method)
        at com.selvas.ocrserver.thread.OcrEngineThread.run(OcrEngineThread.java:57)
        at java.util.concurrent.ThreadPoolExecutor.runWorker(ThreadPoolExecutor.java:1149)
        at java.util.concurrent.ThreadPoolExecutor$Worker.run(ThreadPoolExecutor.java:624)
        at java.lang.Thread.run(Thread.java:748)
~~~

> **문제 해결**
>
> 실행 쉘 스크립트에 라이브러리 경로를 적용하니 정상적으로 위치 설정 완료
>

~~~bash
LD_LIBRARY_PATH=/app/selvy/bin:/usr/local/lib:/usr/lib
export LD_LIBRARY_PATH
java ... -XshowSettings:properties -jar ...war # java.library.path 확인 가능
~~~

