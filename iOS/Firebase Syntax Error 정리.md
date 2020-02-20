# Firebase Sytax Error 정리 - ObjectiveC

이 글은 ObjectiveC에서 Firebase을 사용하며 발생했던 Sytax Error들의 대해 정리한 글이다.

앞으로 발생하는 Error에 대해서도 업데이트는 계속된다.

<br />

<br />

```objective-c
Terminating app due to uncaught exception 'InvalidPathValidation', reason: '(child:) Must be a non-empty string and not contain '.' '#' '$' '[' or ']''
```

Firebase Database에 데이터를 저장할 때 `'.' '#' '$' '[' or ']''` 다음과 같은 특수 문자는 불가능 하다.