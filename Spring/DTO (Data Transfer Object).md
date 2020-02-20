### DTO (Data Transfer Object)

DTO(Data Transfer Object)는 VO(Value Object)로 바꿔 말할 수 있는데 계층 간 데이터 교환을 위한 자바빈즈를 말합니다.

여기서 말하는 계층 간의 Controller, View, Business Layer, Persistent Layer를 말하며 각 계층 간 데이터 교환을 위한 객체를 DTO 또는 VO라고 부릅니다. `그런데 VO는 DTO와 같은 개념이지만 read only 속성을 가짐`

일반적인 DTO는 로직을 갖고 있지 않은 순수한 데이터 객체이며 속성과 그 속성에 접근하기 위한 getter, setter 메소드만 가진 클래스를 말합니다.