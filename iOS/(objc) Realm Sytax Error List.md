# Realm Sytax Error 정리 - ObjectiveC

이 글은 ObjectiveC에서 Realm을 사용하며 발생했던 Sytax Error들의 대해 정리한 글이다.

앞으로 발생하는 Error에 대해서도 업데이트는 계속된다.

<br />

<br />

~~~objective-c
 Terminating app due to uncaught exception 'RLMException', reason: 'Binary too big'
~~~

- 저장하려는 데이터 크기가 16MB를 넘었을 때 나타나는 에러이다.

- 갤러리의 이미지를 Realm에 NSData로 넣는 도중 발생

- NSData.length로 데이터의 크기를 확인할 수 있음

  (18752515 / 1024 / 1024 = 17.88 MB)

<br />

<br />

~~~objective-c
Terminating app due to uncaught exception 'RLMException', reason: 'Property 'test' is declared as 'NSArray', which is not a supported RLMObject property type. All properties must be primitives, NSString, NSDate, NSData, NSNumber, RLMArray, RLMLinkingObjects, or subclasses of RLMObject. See https://realm.io/docs/objc/latest/api/Classes/RLMObject.html for more information.'
~~~

- Realm Property의 자료형을 정의할 때 NSArray 정의했지만, 정의할 수 없다는 에러이다.
- NSString, NSDate, NSData, NSNumber, RLMArray, RLMLinkingObjects 등 Realm에서 지원하는 자료형만 가능

<br />

<br />

~~~~objc
Terminating app due to uncaught exception 'RLMException', reason: 'Property 'test' requires a protocol defining the contained type - example: RLMArray<Person>.'
~~~~

- RLArray로 자로형을 바꿨는데, 해당 자료형은 RLMObject를 상속 받은 서브클래스들로만 객체를 담을 수 있다.

<br />

<br />

# RLArray 사용 문법

일반적으로 Array를 정의할때는 다음과 같이 작성한다.

~~~objc
@property RLMArray<PhotoModel*> *test;
~~~

하지만 Objective-C Realm 버전에서는 다음과 같이 변경해야 문법 에러없이 정상 동작한다.

~~~objc
RLM_ARRAY_TYPE(PhotoModel)
@property RLMArray<PhotoModel *><PhotoModel> *test;
~~~