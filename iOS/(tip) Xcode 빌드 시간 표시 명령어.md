# Xcode 빌드 시간 표시 명령어

1. 터미널로 이동해서 다음 명령어를 입력합니다.

~~~bash
$ defaults write com.apple.dt.Xcode ShowBuildOperationDuration -bool YES
~~~

2. Xcode 재시작을 합니다.
3. `Command + b`를 누르면 빌드가 되면서 시간이 표시됩니다.

<br />

![BuildSecond](../

s/BuildSecond.png)