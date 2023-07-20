---
title: "dart-01 variable"
date: 2023-07-20T21:25:21+09:00
draft: false
categories: [dart,language]
tags: [dart,flutter,nomadcoder]
ShowToc: true
comments: true
---
with [https://nomadcoders.co/dart-for-beginners](https://nomadcoders.co/dart-for-beginners)
  
## Var Keyword
```
void main() {
  var name = '니꼬';
  // name이 문자열로 초기화 됐을 때 후에 다른 타입(정수형)을 넣을 수 없음
  // name = 1; 
  // 문자열은 가능
  name = 'nico';

  // 타입을 지정해서 사용할 수 도 있음
  String name1 = '니꼬';
  int i = 1;

  // 관습적으로?
  // 함수나 메소드 내부에서 지역변수를 선언할 때에는 var를 사용
  // class 내 property 변수는 타입을 지정
}
```

## Dynamic Type
```
void main() {
  // var로 선언하고 값을 넣지 않으면 dynamic type이 됨
  var name;
  // type 상관 없이 사용 가능
  name = 'nico';
  name = 12;
  name = true;

  // dynamic 이라고 선언 가능
  dynamic name1;

}
```

## Nullable Variable
```
// null safety가 없다면 아래 코드는 런타임(실행중)에 NoSuchMethodError가 발생
// bool isEmpty(String string) => string.length == 0;
// main() {
//   isEmpty(null);
// }

// dart에서는 어떤 변수가 null이 될 수 있는지 정확히 표시해야함
void main() {
  String nico = 'nico';
  // 아래 코드는 불가능함 
  // nico = null; X

  // '?' 를 붙이면 null을 사용할 수 있음
  String? nico1 = 'nico1';
  nico1 = null;
  
  // 'nico'란 변수가 null이 아닌경우 isNotEmpty값을 리턴
  nico?.isNotEmpty;
  // 위 한줄과 같은 표현
  if (nico != null) {
    nico.isNotEmpty;
  }
}
```

## Final Variable
```
// 한번 값을 넣게 되면 수정할 수 없는 변수
void main() {
  final nico = 'nico';
  // final로 선언 했기 때문에 값 변경이 불가능함
  // nico = 'test'; X
}
```

## Late Variable
```
// 값 초기화 없이 변수를 선언하고 나중에 값을 지정할 수 있음
// var 나 final 앞에 붙여줄 수 있는 수식어
void main() {
  // 값을 넣지 않으면 null로 기본값이 들어가는데 late를 이용하여 나중에 값을 지정해줄 수 있다.
  late String nico;
  late final String nico1;
  // print(nico);
  nico = 'nico';
  nico1 = 'nico';

  late final String nico2;
  nico2 = 'nico';
  print(nico2);

  String name;
  // print(name);
  name = '123';
}
```
late를 붙여 선언한 변수와 late 없이 선언한 변수 둘다 사용이 가능했는데 print 구문을 넣고 실행해보니 에러 문구에서 차이가 났다.
```
> dart run main.dart
main.dart:7:9: Error: Late variable 'nico' without initializer is definitely unassigned.
  print(nico);
        ^^^^
main.dart:16:9: Error: Non-nullable variable 'name' must be assigned before it can be used.
  print(name);
        ^^^^
```

## Constant Variable
```
void main() {
    // 컴파일 할 떄 알 수 있는 값으로 final 처럼 값을 한번만 지정 가능.
    // 컴파일 후에 알 수 있는 값으로는 사용 못함. ex) const API = getAPIKey(); X
    const API = '121212';
}
```
