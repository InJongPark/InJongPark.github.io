---
title: "dart-04 Classes"
date: 2023-07-23T15:57:50+09:00
draft: false
categories: [dart,language]
tags: [dart,flutter,nomadcoder]
ShowToc: true
comments: true
---

## Your First Dart Class
```dart
class Player {
  String name = 'nico';
  final int xp = 1500;

  void sayHello() {
    // print("Hi my name is $this.name"); this는 안써도 됨
    print("Hi my name is $name");
  }
}

void main() {
  // var player = new Player(); new 생략 가능
  var player = Player();
  print(player.name);
  player.name = 'lala';
  print(player.name);

  player.sayHello();
}
```

## Constructors
```dart
class Player {
  late final String name;
  late int xp;

  // 생성자
  Player(String name, int xp) {
    this.name = name;
    this.xp = xp;
  }

  void sayHello() {
    print("Hi my name is $name");
  }
}

// 위 를 줄여 아래와 같은 형태로 사용할 수 도 있음
class Player2 {
  final String name;
  int xp;

  Player2(this.name, this.xp);

  void sayHello() {
    print("Hi my name is $name");
  }
}

void main() {
  var player = Player('nico', 1500);
  player.sayHello();
  var player2 = Player('lynn', 1500);
  player2.sayHello();
}
```

## Named Constructor Parameters
```dart
class Player {
  final String name;
  int xp;
  String team;
  int age;

  // {} 중괄호를 사용
  Player({
    required this.name,
    required this.xp,
    required this.team,
    required this.age,
  });

  void sayHello() {
    print("Hi my name is $name");
  }
}

void main() {
  var player = Player(
    name: 'nico',
    xp: 1500,
    team: 'blue',
    age: 12,
  );
  player.sayHello();
  var player2 = Player(
    name: 'nico',
    xp: 1500,
    team: 'blue',
    age: 12,
  );
  player2.sayHello();
}
```

## Named Constructors
```dart
class Player {
  final String name;
  int xp, age;
  String team;

  Player({
    required this.name,
    required this.xp,
    required this.team,
    required this.age,
  });

  // 기본 생성자 외에 다른 생성자 구현
  Player.createBluePlayer({
    required String name,
    required int age,
  })  : this.age = age,
        this.name = name,
        this.team = 'blue',
        this.xp = 0;

  Player.createRedPlayer({
    required String name,
    required int age,
  })  : this.age = age,
        this.name = name,
        this.team = 'red',
        this.xp = 0;

  void sayHello() {
    print("Hi my name is $name");
  }
}

void main() {
  var player = Player.createBluePlayer(
    name: 'nico',
    age: 12,
  );
  player.sayHello();
  var player2 = Player.createRedPlayer(
    name: 'nico',
    age: 13,
  );
  player2.sayHello();
}
```

## Recap
```dart
class Player {
  final String name;
  int xp;
  String team;

  Player.fromJson(Map<String, dynamic> playerJson)
      : name = playerJson['name'],
        xp = playerJson['xp'],
        team = playerJson['team'];

  void sayHello() {
    print("Hi my name is $name");
  }
}

void main() {
  // api를 통해 Json 데이터를 받아왔다고 가정하면 생성자로 바로 초기화해서 사용할 수 있음.
  // flutter에서 많이 보일 패턴이라고 함
  var apiData = [
    {
      'name': 'nico',
      'team': 'red',
      'xp': 0,
    },
    {
      'name': 'lynn',
      'team': 'red',
      'xp': 0,
    },
    {
      'name': 'dal',
      'team': 'red',
      'xp': 0,
    }
  ];
  apiData.forEach((playerJson) {
    var player = Player.fromJson(playerJson);
    player.sayHello();
  });
}
```

## Cascade Notation
```dart
class Player {
  String name, team;
  int xp;

  Player({
    required this.name,
    required this.xp,
    required this.team,
  });

  void sayHello() {
    print("Hi my name is $name");
  }
}

void main() {
  var nico = Player(name: 'nico', xp: 1500, team: 'red');
  nico.name = 'las';
  nico.xp = 12313212;
  nico.team = 'blue';

  // 생성자로 생성 후 바로 값을 변경할 때 .. 사용
  var nico2 = Player(name: 'nico', xp: 1500, team: 'red')
    ..name = 'las'
    ..xp = 12313212
    ..team = 'blue';

  var nico3 = Player(name: 'nico', xp: 1500, team: 'red')
    ..name = 'las'
    ..xp = 12313212
    ..team = 'blue'
    ..sayHello();
}
```

## Enums
```dart
// 미리 사용할 수 있는 요소들을 선언하여 제한함
enum Team { red, blue }

enum XPLevel { beginner, medium, pro }

class Player {
  String name;
  XPLevel xp;
  Team team;

  Player({
    required this.name,
    required this.xp,
    required this.team,
  });

  void sayHello() {
    print("Hi my name is $name");
  }
}

void main() {
  var nico = Player(name: 'nico', xp: XPLevel.beginner, team: Team.blue)
    ..xp = XPLevel.medium
    ..team = Team.red;
}
```

## Abstract Classes
```dart
// 추상화 클래스
// 메소드 내용은 없고 선언만 함
// 다른 클래스들의 blue print
abstract class Human {
  void walk();
}

enum Team { red, blue }

enum XPLevel { beginner, medium, pro }

class Player extends Human {
  String name;
  XPLevel xp;
  Team team;

  Player({
    required this.name,
    required this.xp,
    required this.team,
  });

  void sayHello() {
    print("Hi my name is $name");
  }

  @override
  void walk() {
    // TODO: implement walk
    print("$name is walk.");
  }
}

class Coach extends Human {
  @override
  void walk() {
    // TODO: implement walk
    print('The coach is walk');
  }
}

void main() {
  var nico = Player(name: 'nico', xp: XPLevel.beginner, team: Team.blue)
    ..xp = XPLevel.medium
    ..team = Team.red;

  nico.walk();
}
```

## Inheritance
```dart
class Human {
  final String name;
  Human(this.name);
  void sayHello() {
    print('Hi my name is $name');
  }
}

enum Team { red, blue }

// 상속받아서 Human에 있는 모든 요소들을 포함
class Player extends Human {
  final Team team;
  // name 을 받아서 super(Human 부모 클래스의 생성자) 실행
  Player({
    required this.team,
    required String name,
  }) : super(name);

  @override
  void sayHello() {
    // TODO: implement sayHello
    super.sayHello();
    print('and I play for $team!');
  }
}

void main() {
  var player = Player(team: Team.red, name: 'nico');
  player.sayHello();
}
```

## Mixins
```dart
// Mixin: 생성자가 없는 클래스
mixin Strong {
  final double strengthLevel = 1500.99;
}

mixin QuickRunner {
  void runQuick() {
    print('ruuuunnn!!!!');
  }
}

mixin Tall {
  final double height = 1.99;
}

enum Team { red, blue }

class Player with Strong, QuickRunner, Tall {
  Team team;

  Player({
    required this.team,
  });
}

class Horse with Strong, QuickRunner {}

class Kid with QuickRunner {}

void main() {
  var player = Player(team: Team.red);
  player.runQuick();
}
```