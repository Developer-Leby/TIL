# Foundation Framework 정리

Foundation 프레임워크는 애플에서 기본적으로 제공하는 프레임워크이고, 다양한 객체 컬렉션을 제공한다.

> #import <Foundation/Foundation.h>

다음과 같이 헤더파일을 임포트를 하면 Foundation 객체를 사용할 수 있다.

<br />

<br />

# NSNumber 객체

NSNumber 클래스는 초기값을 지정하여 객체를 생성하는 메서드들이 있다.

~~~objc
NSNumber *intNumber = [NSNumber numberWithInteger: 100];
NSInteger myInt = [intNumber integerValue];
~~~

