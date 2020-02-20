# NSTimer 사용하기

프로그래밍을 하다 보면 특정 작업이 **몇초, 몇분, 몇시간** 후에 실행되는 **로직을 원할 때**가 있습니다. 이런 경우에 `dispatch_after`를 사용해서 처리할 수도 있지만, 또 다른 방법으로는 `NSTimer`를 이용하면 **편리하게 구현**할 수 있습니다.

~~~objective-c
// dispatch_after 사용하는 경우
dispatch_time_t waitTime = dispatch_time(DISPATCH_TIME_NOW, CALL_INTERVAL * NSEC_PER_SEC);
dispatch_after(waitTime, dispatch_get_global_queue( DISPATCH_QUEUE_PRIORITY_HIGH, 0), ^(void) {
    
});
~~~

`dispatch_after`의 경우 `NSDictionary`형태의 데이터를 넘길 수 없는데 `NSTimer`는 `Dictionary`형태의 데이터를 전달할 수 있습니다. 그러면 `NSTimer`를 사용하는 방법에 대해 알아보도록 하겠습니다.

<br />

~~~objective-c
NSDictionary *userInfo = @{@"USER_NAME":@"Leby.Y.Kim"};
NSTimer *timer = [NSTimer scheduledTimerWithTimeInterval:5
                                                  target:self
                                                selector:@selector(timerHandler:)
                                                userInfo:userInfo
                                                 repeats:NO]; //5초
~~~

위 방법처럼 작성하면 `NSTimer`를 등록하고 메서드가 실행이 됩니다. 설명은 아래와 같습니다.

~~~objective-c
Interval:5	// 5초 뒤에 실행
target:self	// 현재 클래스
selector:@selector(timerHandler:)	 // 5초 뒤 실행되는 메서드
userInfo:userInfo	// 전달할 Dictionary 데이터
repeats:NO	 // 반복 여부
~~~

타이머의 의해 실행되는 메서드 구현

~~~objective-c
-(void)timerHandler:(NSTimer*)timer
{
    NSDictionary *userInfo = (NSDictionary*)timer.userInfo;
    NSString *value = [userInfo objectForKey:@"USER_NAME"];
    NSLog(@"value: %@", value);
    
    [timer invalidate];
}
~~~

`timerHandler` 메서드에는 `userInfo`로 받은 ` Dictionary`데이터를 **KEY**값을 이용해서 가져와 출력합니다.

<br />

`[timer invalidate];` 타이머가 계속 메모리에 남아있으면 안되니 **타이머를 종료하는 메서드**입니다.