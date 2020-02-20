# Objective-C Style Guide 정리

이 스타일 가이드는 NYTimes의 iOS팀의 코딩 규칙에 대해 설명해 놓은 것을 개인적인 공부 목적으로 정리 해놓은 것입니다.

또한 제 생각에 필요하지 않은 부분들은 빠져있으니 자세한 내용은 아래 링크를 통해 확인하시면 됩니다.

https://github.com/NYTimes/objective-c-style-guide

<br />

<br />

# 점 표기법 구문 (Dot Notation Syntax)

객체의 속성을 가져오고 설정하기 위해 괄호 표기법보다 점 표기법을 권장합니다.

**올바른 예 :**

~~~~obj
view.backgroundColor = [UIColor orangeColor];
[UIApplication sharedApplication].delegate;
~~~~

**~~틀린 예 :~~**

~~~~objc
[view setBackgroundColor:[UIColor orangeColor]];
UIApplication.sharedApplication.delegate;
~~~~

<br />

<br />

# 간격 (Spacing)

- 들여 쓰기는 반드시 4칸을 사용해야합니다. 이 환경 설정은 Xcode에서 설정해야합니다.
- 메서드 중괄호와 다른 중괄호 (if/else/switch/while 등)문은 동일한 줄에서 열어야합니다.

**올바른 예 :**

~~~~objc
if (user.isHappy) {
     // Do something 
} else {
     // 다른 작업을 수행 
}
~~~~

<br />

<br />

# 조건부 (Conditionals)

조건부 본문은 오류를 방지하기 위해 중괄호 없이 한 줄로만 작성할 수 있는 경우에도 중괄호를 사용해야합니다.

중괄호 없이 한 줄로만 작성할 경우 두번째 줄이 if문에 포함되는 것과 같이 코딩을 한다면 에러가 발생할 수 있습니다.

또한, 이러한 스타일은 다른 조건과 일관성이 있으므로 스캔하기 쉬워서 오류를 방지할 수 있습니다.

**올바른 예 :**

~~~~objc
if (!error) {
    return success;
}
~~~~

**~~틀린 예 :~~**

~~~~objc
if (!error)
    return success;
~~~~

또는

~~~objc
if (!error) return success;
~~~

<br />

<br />

# 삼항 연산자 (Ternary Operator)

삼항 연산자의 목적은 코드를 깔끔하게 보이도록하는데 있습니다.

삼원 항은 표현식 당 하나의 조건만을 평가해야합니다. 

여러 조건을 평가할 때는 차라리 if문이나 명명된 변수로 리팩터링 하는 것이 더 이해하기 쉽습니다.

**올바른 예 :**

~~~~objc
result = a > b ? x : y;
~~~~

**~~틀린 예 :~~**

~~~~objc
result = a > b ? x = c > d ? c : d : y;
~~~~

<br />

<br />

# 오류 처리 (Error Handling)

메서드가 참조로 오류 매개 변수를 반환하면 코드는 반환된 값을 전환해야합니다.

**올바른 예 :** 

~~~~objc
NSError *error;
if (![self trySomethingWithError:&error]) {
    // Handle Error
}
~~~~

**~~틀린 예 :~~**

~~~~objc
NSError *error;
[self trySomethingWithError:&error];
if (error) {
    // Handle Error
}
~~~~

Apple의 API 일부는 성공한 경우 error 매개 변수에 nil 값이 아닌 경우 쓰레기 값을 넣음으로써 error가 false라고 인식해서

부정적인 결과를 초래할 수 있습니다.

<br />

<br />

# 메서드 (Methods)

메서드는 시그니쳐에는 (- 또는 + 심볼) 다음에 공백이 있어야 합니다.

메서드 세그먼트 사이에도 공백이 있어야 합니다.

**올바른 예 :**

~~~~objc
- (void)setExampleText:(NSString *)text image:(UIImage *)image;
~~~~

~~~objc
- (void)setExampleText:(NSString *)text 
                 image:(UIImage *)image 
                 color:(UIColor *)color 
       alternativeText:(NSString *)altText;
~~~

80자를 초과하는 메소드는 각 인수 뒤에 새로운 행이있는 양식처럼 보여지도록 합니다.

<br />

<br />

# 변수 (Variables)

변수는 설명 적으로 명명되어야 하며, 변수의 이름은 변수가 무엇이고 어떤 의미인지를 명확하게 전달하고

프로그래머가 해당 값을 적절하게 사용하기 위해서는 필요한 정보를 포함해야 합니다.

**올바른 예 :**

- `NSString *title` : 제목 문자열입니다.
- `NSString *titleHTML` : HTML의 제목 문자열입니다.
- `NSAttributedString *titleAttributedString` : 제목의 속성을 추가하기 위한 문자열입니다.
- `NSDate *now` : 현재 날짜 정보를 담고 있습니다.

타입에서 (*)는 변수 이름에 붙어야합니다.  

**예를 들어**,

~~~~objc
NSString *text;
NSString* text;
NSString * text;
NSString * const NYTConstantString;
~~~~

이런식으로 사용됩니다.

속성 정의는 가능하다면 인스턴스 변수를 직접 접근 하는 방법이 아닌 다음 과 같은 초기화 방법을 사용해야 합니다.

(`Init`, `initWithCoder`, `dealloc`, `getter`, `setter` 등) 을 이용해야 합니다.

**올바른 예 :**

~~~~objc
@interface NYTSection : NSObject

@property (nonatomic) NSString *headline;

@end
~~~~

**~~틀린 예 :~~**

~~~~objc
@interface NYTSection : NSObject {
    NSString *headline;
}
~~~~

ARC가 도입되고 부터는 변수를 선언할 때 다음 항목들이 이름 사이에 위치 해야합니다.

(`__strong`, `__weak`,  `__unsafe_unretained`, `__autoreleasing`)

**올바른 예 :**

~~~objc
NSString * __weak text
~~~

<br />

<br />

# 이름 규칙 (Naming)

이름만으로도 어떤 변수인지를 알 수 있는 설명이 포함된 변수 이름이 좋습니다.

변수의 이름이 길다고 해서 맘대로 줄여쓰는 오히려 헷갈릴 수 있습니다.

**올바른 예 :** 

````objc
UIButton *settingsButton;
````

**~~틀린 예 :~~** 

```objc
UIButton *setBut
```

<br />

<br />

# init과 dealloc 메서드

`dealloc` 메서드는 구현의 맨 위에 있는 `@synthesize`와 `@dynamic`문 바로 뒤에 있어야 합니다.

`init` 메서드는 클래스의 바로 아래에 위치해야 합니다.

~~~~objc
- (instancetype)init {
    self = [super init]; // or call the designated initializer
    if (self) {
        // Custom initialization
    }
    return self;
}
~~~~

<br />

<br />

# 리터럴 (Literals)

`NSString`, `NSDictionary`, `NSArray`, `NSNumber` 등 인스턴스 값이 변하지 않을 경우 리터럴을 이용하여 값을 줄 수 있습니다.

**올바른 예 :** 

~~~obj
NSArray *names = @[@"Brian", @"Matt", @"Chris", @"Alex", @"Steve", @"Paul"];
NSDictionary *productManagers = @{@"iPhone": @"Kate", @"iPad": @"Kamal", @"Mobile Web": @"Bill"};
NSNumber *shouldUseLiterals = @YES;
NSNumber *buildingZIPCode = @10018;
~~~

**~~틀린 예 :~~**

~~~objc
NSArray *names = [NSArray arrayWithObjects:@"Brian", @"Matt", @"Chris", @"Alex", @"Steve", @"Paul", nil];
NSDictionary *productManagers = [NSDictionary dictionaryWithObjectsAndKeys: @"Kate", @"iPhone", @"Kamal", @"iPad", @"Bill", @"Mobile Web", nil];
NSNumber *shouldUseLiterals = [NSNumber numberWithBool:YES];
NSNumber *buildingZIPCode = [NSNumber numberWithInteger:10018];
~~~

<br />

<br />

# CGRect 기능

`CGRect`에 width, height, x, y의 값을 액세스하고 싶은 경우 바로 변수 값에 접근하는 방법보다 지원해주는 함수를 사용하여

값을 액세스 하는 것을 선호합니다.

**올바른 예 :**

~~~~objc
CGRect frame = self.view.frame;

CGFloat x = CGRectGetMinX(frame);
CGFloat y = CGRectGetMinY(frame);
CGFloat width = CGRectGetWidth(frame);
CGFloat height = CGRectGetHeight(frame);
~~~~

**~~틀린 예 :~~**

~~~~objc
CGRect frame = self.view.frame;

CGFloat x = frame.origin.x;
CGFloat y = frame.origin.y;
CGFloat width = frame.size.width;
CGFloat height = frame.size.height;
~~~~

