# Swipe Gesture 정리

iOS는 SDK에서는 많은 제스처를 알 수 있지만, 그 중에서도 스와이프 제스처에 대해 정리하려 합니다.

<br />

# Swipe Gesture 등록

~~~swift
// Swift
override func viewDidLoad() {
    super.viewDidLoad()
        
    let leftSwipeGestureRecognizer = UISwipeGestureRecognizer(target: self, action: #selector(handleSwipes(_:)))
    let rightSwipeGestureRecognizer = UISwipeGestureRecognizer(target: self, action: #selector(handleSwipes(_:)))
        
    leftSwipeGestureRecognizer.direction = .left
    rightSwipeGestureRecognizer.direction = .right

    view.addGestureRecognizer(leftSwipeGestureRecognizer)
    view.addGestureRecognizer(rightSwipeGestureRecognizer)
}
~~~

~~~objective-c
// Objective-C
- (void)viewDidLoad {
    [super viewDidLoad];
    
    UISwipeGestureRecognizer *leftSwipeGestureRecognizer = [[UISwipeGestureRecognizer alloc] initWithTarget:self action:@selector(handleSwipes:)];
	UISwipeGestureRecognizer *rightSwipeGestureRecognizer = [[UISwipeGestureRecognizer alloc] initWithTarget:self action:@selector(handleSwipes:)];
    
    leftSwipeGestureRecognizer.direction = UISwipeGestureRecognizerDirectionLeft;    
    rightSwipeGestureRecognizer.direction = UISwipeGestureRecognizerDirectionRight;  
    
    [self.view addGestureRecognizer:leftSwipeGestureRecognizer];
	[self.view addGestureRecognizer:rightSwipeGestureRecognizer];
}
~~~

`UISwipeGestureRecognizer`를 사용해서 왼쪽, 오른쪽 스와이프 제스처를 방향을 정하고 현재 뷰에 추가합니다. 제스처가 감지되면 `handleSwipes` 메서드가 호출되고 메서드에서 제스처 했을 때의 동작을 구현하면 됩니다.

<br />

~~~swift
// Swift
@objc func handleSwipes(_ sender:UISwipeGestureRecognizer) {
    if (sender.direction == .left) {
        NSLog("Swipe Left")
    }
        
    if (sender.direction == .right) {
        NSLog("Swipe Right")
    }
}
~~~

~~~objc
// Objective-C
- (void)handleSwipes:(UISwipeGestureRecognizer*)recognizer {
    if (recognizer.direction == UISwipeGestureRecognizerDirectionLeft) {
        NSLog(@"Swipe Left");
    }
    else if (recognizer.direction == UISwipeGestureRecognizerDirectionRight) {
        NSLog(@"Swipe Right");
    }
}
~~~

`handleSwipes`메서드에서 왼쪽, 오른쪽 Swipe에 대해 동작하는 것을 구현할 수 있습니다.

