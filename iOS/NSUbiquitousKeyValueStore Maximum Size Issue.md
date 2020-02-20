# NSUbiquitousKeyValueStore Maximum Size Issue

iCloud에 동기화를 구현하면서 Key-Value를 저장하는 `[NSUbiquitousKeyValueStore defaultStore] `를 사용하다

이미지를 NSData 형태로 저장하고 다시 불러오는 과정에서 못 불러오는 이슈가 생겼다.

로직에 문제가 있는가? 하고 테스트 샘플을 만들어 진행해보고 확인해봤는데 데이터가 저장되지 않는 이슈가 생겼다.

<br />

<br />

그래서 NSUbiquitousKeyValueStore [애플 도큐먼트 확인](https://developer.apple.com/library/archive/documentation/Cocoa/Conceptual/UserDefaults/StoringPreferenceDatainiCloud/StoringPreferenceDatainiCloud.html)를 확인해보니 안되는 이유가 있었다.

Key-Value 형태로 저장하는 방식에는 다음과 같이 조건들이 있었다.

-  앱은 키 - 값 저장소에 1MB의 전체 공간으로 제한됩니다. 키당 별도로 1MB 제한이 있으며 최대 1024 개의 키가 허용됩니다. 따라서 키 - 값 저장소를 사용하여 많은 양의 데이터를 공유 할 수 없습니다.
- 키 - 값 저장소는 속성 목록 유형 만 지원합니다. 속성 목록 유형은 단순과 같은 유형을 포함 `NSNumber`, `NSString`및 `NSDate`객체. 원시 데이터 블록을 `NSData`객체에 저장 `NSArray`하고 `NSDictionary`객체 와객체를 사용하여 모든 유형을 정렬 할 수도 있습니다 .
- 키 - 값 저장소는 변경 빈도가 낮은 데이터를 저장하기위한 저장소입니다. 기기의 앱이 키 - 값 저장소를 자주 변경하면 시스템은 서버에 대한 왕복 횟수를 최소화하기 위해 일부 변경 사항의 동기화를 지연시킬 수 있습니다.앱이 자주 변경 될수록 나중에 변경 사항이 지연되어 다른 기기에 즉시 표시되지 않을 가능성이 커집니다.
- 키 - 값 저장소는 동일한 데이터를 저장하기위한 기본 설정이나 다른 로컬 기술을 대체하지 않습니다. 키 - 값 저장소의 목적은 앱간에 데이터를 공유하는 것이지만 iCloud가 활성화되지 않았거나 특정 장치에서 사용할 수없는 경우에도 여전히 데이터의 로컬 복사본을 보관할 수 있습니다.

<br />

<br />

# 결론

Key-Value의 저장소의 전체 공간은 1MB 크기로써 갤러리에 JPEG 이미지 기준으로 4~5개 정도면 1MB를 넘어가기 때문에

저장이 안 됐던 이슈가 생겼던 것이다.

iCloud에 큰 사이즈에 데이터를 저장할 때에는 Key-Value 저장 전략이 아닌 Document 저장으로 구현 해야될 것 같다.