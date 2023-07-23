---
title: "dart-03 Function"
date: 2023-07-23T15:50:53+09:00
draft: false
categories: [dart,language]
tags: [dart,flutter,nomadcoder]
ShowToc: true
comments: true
---

## Defining a Function
```dart
void sayHello(String name) {
  print("Hello $name, nice to meet you!");
}

String sayHello2(String name) {
  return "Hello $name, nice to meet you!";
}

String sayHello3(String name) => "Hello $name, nice to meet you!";

void main() {
  sayHello('nico');
  print(sayHello2('nico'));
  print(sayHello3('nico'));
}
```

## Named Parametes
```dart
// positional parameter
String sayHello(String name, int age, String country) {
  return "Hello $name, you are $age, and you come from $country";
}

// 파라미터에 중괄호를 추가하면 named parameter로 사용이 가능
// default value가 없으면 파라미터 값이 null이 될 수 있기 때문에 실행이 안됨
String sayHello2({String name = '', int age = 0, String country = ''}) {
  return "Hello $name, you are $age, and you come from $country";
}

// default value를 지정하지 않고 데이터를 받아야만 한다면 required 를 추가하면 됨
String sayHello3({required name, required int age, required String country}) {
  return "Hello $name, you are $age, and you come from $country";
}

void main() {
  print(sayHello('nico', 12, 'cuba'));
  print(sayHello2(
    age: 12,
    country: 'cuba',
    name: 'nico',
  ));
  print(sayHello2());
  print(sayHello3(
    age: 12,
    country: 'cuba',
    name: 'nico',
  ));
}
```

## Recap
```dart
// positional parameter
String sayHello(String name, int age, String country) {
  return "Hello $name, you are $age, and you come from $country";
}

// 파라미터에 중괄호를 추가하면 named parameter로 사용이 가능
// default value가 없으면 파라미터 값이 null이 될 수 있기 때문에 실행이 안됨
String sayHello2({String name = '', int age = 0, String country = ''}) {
  return "Hello $name, you are $age, and you come from $country";
}

// default value를 지정하지 않고 데이터를 받아야만 한다면 required 를 추가하면 됨
String sayHello3({required name, required int age, required String country}) {
  return "Hello $name, you are $age, and you come from $country";
}

void main() {
  print(sayHello('nico', 12, 'cuba'));
  // positional parameter라서 순서가 다르면 실행이 안됨
  // print(sayHello(12, 'nico', 'cuba')); X
  print(sayHello2(
    age: 12,
    country: 'cuba',
    name: 'nico',
  ));
  print(sayHello2());
  print(sayHello3(
    age: 12,
    country: 'cuba',
    name: 'nico',
  ));
}
```

## Optional Positional Parameters
```dart
// optional positional parameter
// [] 대괄호로 감싸면 optional
String sayHello(String name, int age, [String? country]) =>
    "Hello $name, you are $age, and you come from $country";

String sayHello2(String name, int age, [String? country = 'cuba']) =>
    "Hello $name, you are $age, and you come from $country";

String sayHello3(String name, int age, String? country) =>
    "Hello $name, you are $age, and you come from $country";

void main() {
  print(sayHello('nico', 12));
  print(sayHello2('nico', 12));
}
```
country 값이 null 이 가능하도록 했지만 실제 실행하니 에러나 남
```shell
print(sayHello3('nico', 12)); X
❯ dart run main.dart
main.dart:15:18: Error: Too few positional arguments: 3 required, 2 given.
  print(sayHello3('nico', 12));
                 ^
main.dart:9:8: Context: Found this candidate, but the arguments don't match.
String sayHello3(String name, int age, String? country) =>
       ^^^^^^^^^
```

## QQ Operator
```dart
String capitalizeName(String name) => name.toUpperCase();

// name이 null 일 수 있기 때문에 toUpperCase를 바로 사용 못함.
// String capitalizeName2(String? name) => name.toUpperCase();

String capitalizeName2(String? name) {
  if (name != null) {
    return name.toUpperCase();
  }
  return 'NONE';
}

String capitalizeName3(String? name) =>
    name != null ? name.toUpperCase() : 'NONE';

// ?? -> Left ?? Right -> Left가 null이면 Right를 return함
String capitalizeName4(String? name) => name?.toUpperCase() ?? 'NONE';

void main() {
  print(capitalizeName('nico'));

  print(capitalizeName2(null));

  String? name;
  // name이 null이면 오른쪽 값을 적용
  name ??= 'nico';
}
```

## Typedef
```dart
List<int> reverseListOfNumbers(List<int> list) {
  var revered = list.reversed;
  return revered.toList();
}

// typedef로 자료형을 선언해서 다른곳에서 alias 처럼 사용이 가능
typedef ListOfInts = List<int>;
ListOfInts reverseListOfNumbers2(ListOfInts list) {
  var revered = list.reversed;
  return revered.toList();
}

typedef UserInfo = Map<String, String>;
String sayHi(UserInfo userInfo) {
  return "Hi ${userInfo['name']}";
}

void main() {
  print(reverseListOfNumbers(([1, 2, 3])));
  print(reverseListOfNumbers2(([1, 2, 3])));
  print(sayHi({'name': 'nico'}));
}
```
