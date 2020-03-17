## 윈도우10 ISO 다운로드

- [Microsoft Windows 10 ISO Download](https://www.microsoft.com/ko-kr/software-download/windows10ISO)

<br/>

<br/>

## 디스크 유틸리티 실행

- Launchpad > 기타 >디스크 유틸리티

<br/><br/>

## USB 초기화

- 외장 탭 > USB 선택 > 지우기

> 이름 : NO_NAME (적당한 영문이름)
>
> 포멧 : MS-DOS(FAT)

<br/><br/>

## 윈도우10 ISO 마운트

- GUI 환경에서 더블 클릭

<br/><br/>

## 터미널 실행

- 윈도우10 마운트 폴더로 이동

~~~bash
cd /Volumes/CCCOMA_X64FRE_KO-KR_DV9
ls -al
-r-xr-xr-x   1 leby.y.kim  staff   128B 10  7 12:58 autorun.inf
dr-xr-xr-x   5 leby.y.kim  staff   564B 10  7 13:03 boot
-r-xr-xr-x   1 leby.y.kim  staff   400K 10  7 12:58 bootmgr
-r-xr-xr-x   1 leby.y.kim  staff   1.4M 10  7 12:59 bootmgr.efi
dr-xr-xr-x   4 leby.y.kim  staff   148B 10  7 13:03 efi
-r-xr-xr-x   1 leby.y.kim  staff    72K 10  7 12:58 setup.exe
dr-xr-xr-x  12 leby.y.kim  staff    12K 10  7 13:03 sources
dr-xr-xr-x   3 leby.y.kim  staff    96B 10  7 13:03 support
~~~

- 파일 모두 복사 (약 10분~15분 소요)

~~~bash
cp -R * /Volumes/NO_NAME
~~~