# UIImage 이미지를 자를 때 고려할 점

UIImage의 size는 픽셀(px) 단위가 아닌 포인트(point) 단위로 처리된다. 따라서 사이즈 정보에 추가적으로 스케일(scale)정보를 같이 가지고 있다. 그래서 이미지를 자르거나 리사이징 할때는 scale 값을 고려해서 처리를 해야한다.

<br />

예를 들어, 1920 x 1080 사이즈가 있을 때 이미지를 크롭한다고 가정했을 때 CGRect 값을 원하는 사이즈로 적용해야 한다. 하지만 적용할 때 scale 값을 주지 않으면 픽셀(px)단위에서 영역을 잡는게 아니라 포인트(point) 단위로 계산하기 때문에 원하는데로 잘리지 않는 현상이 발생될 수 있다.

<br />

**잘못된 예**

~~~objc
- (UIImage *)crop:(CGRect)rect image:(UIImage *)image {
    if (self.captureImageView.image.scale > 1.0f) {
        rect = CGRectMake(rect.origin.x,
                          rect.origin.y,
                          rect.size.width,
                          rect.size.height);
    }
    
    CGImageRef imageRef = CGImageCreateWithImageInRect(image.CGImage, rect);
    UIImage *result = [UIImage imageWithCGImage:imageRef scale:image.scale orientation:image.imageOrientation];
    CGImageRelease(imageRef);
    return result;
}
~~~

<br />

**올바른 예**

~~~~objc
- (UIImage *)crop:(CGRect)rect image:(UIImage *)image {
    if (self.captureImageView.image.scale > 1.0f) {
        rect = CGRectMake(rect.origin.x * image.scale,
                          rect.origin.y * image.scale,
                          rect.size.width * image.scale,
                          rect.size.height * image.scale);
    }
    
    CGImageRef imageRef = CGImageCreateWithImageInRect(image.CGImage, rect);
    UIImage *result = [UIImage imageWithCGImage:imageRef scale:image.scale orientation:image.imageOrientation];
    CGImageRelease(imageRef);
    return result;
}
~~~~

올바른 예와 같이 Rect값 뿐만 아니라 scale의 값도 적용시켜야 제대로 보인다.