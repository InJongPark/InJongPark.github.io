---
title: "dart-02 Data Types"
date: 2023-07-23T15:38:03+09:00
draft: false
categories: [dart,language]
tags: [dart,flutter,nomadcoder]
ShowToc: true
comments: true
---

## Basic Data Types
```dart
void main() {
  String name = 'nico';
  bool alive = true;
  int age = 12;
  double money = 69.99;

  // 대부분의 데이터 타입들이 객체로 이뤄져 있다.
  // int 및 double의 경우 extends(상속) num 
  // 그래서 아래와 같이 num으로 선언하면 정수와 실수를 모두 사용할 수 있다.
  num x = 12;
  x = 1.1;
}
```

## Lists
```dart
void main() {
  var numbers = [1, 2, 3, 4];
  List<int> numbers2 = [1, 2, 3, 4];
  numbers2.add(5);

  // 마지막 요소에 ','를 넣으면 VS code에서 알아서 아래처럼 포맷해줌
  var number3 = [
    1,
    2,
    3,
    4,
  ];

  // collection if , collection for 를 지원
  // collection if =>
  var giveMeFive = true;
  var number4 = [
    1,
    2,
    3,
    4,
  ];
  if (giveMeFive) {
    number4.add(5);
  }
  var number5 = [
    1,
    2,
    3,
    4,
    if (giveMeFive) 5,
  ];
}
```

## String Interpolcation
```dart
void main() {
  // String Interpolation: text에 변수를 추가하는 방법

  var name = 'nico';
  // $ 뒤에 변수 이름을 넣어 사용하면 되고 ' " 둘중에 아무거나 사용해도 된다.
  var greeting = 'Hello everyone, my name is $name, nice to meet you!';
  var greetin2 = "Hello everyone, my name is $name, nice to meet you!";
  print(greeting);

  // {} 를 사용해서 변수 값을 더해서 사용할 수 도 있음
  var name2 = 'nico';
  var age = 10;
  var greeting3 = "Hello everyone, my name is $name and I'm ${age + 2}";
  print(greeting3);
}
```

## Collection For
```dart
void main() {
  var oldFriends = ['nico', 'lynn'];
  var newFriends = [
    'lewis',
    'ralph',
    'darren',
  ];
  for (var friend in oldFriends) {
    newFriends.add("💖 $friend");
  }
  print(newFriends);

  // collection for
  var oldFriends2 = ['nico', 'lynn'];
  var newFriends2 = [
    'lewis',
    'ralph',
    'darren',
    for (var friend in oldFriends2) "💖 $friend",
  ];
  print(newFriends2);
}
```

## Maps
```dart
void main() {
  // Map<String, Object> 타입
  // Object -> any라고 보면 됨
  var player = {
    'name': 'nico',
    'xp': 19.99,
    'superpower': false,
  };
  // var로 사용하면 컴파일러가 알아서 타입을 지정해주기도 하지만 아래처럼 지정해서 사용해도됨
  Map<int, bool> player2 = {
    1: false,
    2: true,
    3: false,
  };

  List<Map<String, Object>> players = [
    {'name': 'nico', 'xp': 19.99, 'superpower': false},
    {'name': 'nice', 'xp': 19.98, 'superpower': true},
  ];
}
```

## Sets
```dart
void main() {
  // Set<int> 타입
  // Set의 각 요소들은 유니크해야함
  var numbers = {1, 2, 3, 4};
  Set<int> numbers2 = {1, 2, 3, 4};
  numbers.add(1);
  numbers.add(1);
  numbers.add(1);
  print(numbers);

// ❯ dart run main.dart
// {1, 2, 3, 4}
}
```