---
title: "Flutter 00 Settings"
date: 2023-07-23T23:46:23+09:00
draft: true
categories: []
tags: []
ShowToc: true
comments: true
---

### Extension
- Dart
- Flutter
- Error Lens

### Open User Settings (JSON)
settings.json
```json 
"editor.codeActionsOnSave": {
    "source.fixAll": true
},
"editor.formatOnSave": true,
"dart.previewFlutterUiGuides": true,
```

### pub

flutter cors error
```shell
❯ dart pub global activate flutter_cors
## vi ~/.zshrc
## export PATH="$PATH":"$HOME/.pub-cache/bin"
❯ zsh
❯ fluttercors --disable
❯ fluttercors --enable
```
