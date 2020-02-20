# AutoLayout Set Frame Issue

최근에 프로젝트를 진행하며 AutoLayout이 적용된 View A가 있었고, 아무런 제약조건이 없는 View B가 있었다.

제약조건이 없는 View B에 크기를 AutoLayout이 적용된 View A와 동일한 사이즈로 변경하려고 View A의 Frame

사이즈를 넣었더니 사이즈가 변경되지 않았다.

~~~~objective-c
- (void)viewDidAppear:(BOOL)animated {
	viewB.frame = CGRectMake(self.ViewA.frame.origin.x,
                             self.ViewA.frame.origin.y,
                             self.ViewA.frame.size.width,
                             self.ViewA.frame.size.height);
}
~~~~



구글링 결과 AutoLayout이 적용되는 시점은 다음 메서드에서 변경이 된다고 나와있었다.

~~~~objective-c
- (void)viewDidLayoutSubviews;
~~~~



그래서 다음과 같이 소스를 변경하니까 View A 와 View B의 크기가 동일하게 변경된 것을 확인할 수 있었다.

~~~~objective-c
- (void)viewDidLayoutSubviews {
	viewB.frame = CGRectMake(self.ViewA.frame.origin.x,
                             self.ViewA.frame.origin.y,
                             self.ViewA.frame.size.width,
                             self.ViewA.frame.size.height);
}
~~~~
