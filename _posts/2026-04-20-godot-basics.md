---
layout: post
title: "Godot 기초: 노드, 씬, 스크립팅 개념 정리"
date: 2026-04-20 23:30:00 +0900
categories: [game, godot]
tags: [godot, tutorial, gdscript]
---

이 글은 Godot Engine의 핵심 개념(노드, 씬, 인스턴스화, 스크립팅, 입력 처리, 신호 등)을 정리한 기초 가이드입니다. 공식 문서(https://docs.godotengine.org/en/stable/)의 "Step by step" 시리즈와 "Getting started" 섹션을 참고하여 요약했습니다.

## 1. 소개
Godot은 2D/3D 게임을 만들기 위한 오픈소스 엔진입니다. 프로젝트는 노드(Node)와 씬(Scene)을 기본 단위로 사용하며, 이들로 계층적 구조를 구성합니다. 스크립트는 GDScript(기본), C#, VisualScript 등을 지원합니다.

## 2. 노드와 씬
- 노드(Node): Godot의 모든 오브젝트는 노드입니다. 노드는 특정 기능을 수행하도록 설계됩니다. 예: Node2D, Sprite, Camera2D, CollisionShape2D 등.
- 씬(Scene): 노드 트리(루트 노드와 자식들)로 구성된 단위입니다. 씬은 별도 파일(.tscn)로 저장되어 재사용/인스턴스화할 수 있습니다.

## 3. 씬 인스턴스화
- 씬을 다른 씬에 인스턴스로 추가하여 재사용합니다.
- 에디터에서 Drag & Drop 또는 코드에서 `load("res://path/to/scene.tscn").instantiate()` 를 사용합니다.

```gdscript
var PackedScene = preload("res://Player.tscn")
var player_instance = PackedScene.instantiate()
add_child(player_instance)
```

## 4. 스크립팅 (GDScript)
- GDScript는 Python과 유사한 문법을 가지며, Godot에 최적화된 언어입니다.
- 파일 확장자는 `.gd`이며 `extends` 키워드를 사용하여 노드를 확장합니다.

```gdscript
extends Node2D

func _ready():
    print("Hello, Godot")

func _process(delta):
    # 매 프레임 호출
    pass
```

## 5. 입력 처리
- `Input` 싱글턴을 사용하거나 `_input(event)` 콜백을 구현합니다.

```gdscript
if Input.is_action_pressed("ui_right"):
    position.x += 100 * delta

func _input(event):
    if event is InputEventKey and event.pressed:
        print(event.scancode)
```

## 6. 신호(Signals)
- 신호는 노드 간 통신을 위한 이벤트 시스템입니다. 노드는 내장 신호를 제공하거나 사용자 정의 신호를 선언할 수 있습니다.

```gdscript
signal health_changed(new_health)
emit_signal("health_changed", current_health)
# 연결 예: some_node.connect("health_changed", self, "on_health_changed")
```

## 7. 리소스와 파일 구조
- 프로젝트 루트에 `project.godot` 파일이 있고, 씬(.tscn), 스크립트(.gd), 리소스(이미지, 오디오) 등은 `res://` 경로 기준으로 관리됩니다.
- 권장 폴더 구조 예:
```
res://
  scenes/
    level1.tscn
    player.tscn
  scripts/
    player.gd
  assets/
    sprites/
    sounds/
```

## 8. 에디터 팁
- 씬 트리를 적극 활용해 작은 단위의 씬을 만들고 인스턴스화하세요.
- 디버그 옵션(Visible Collision Shapes 등)을 사용해 물리 디버깅을 하세요.

## 9. 참고 자료
- Official Docs: https://docs.godotengine.org/en/stable/
- Step by step: Getting started tutorials
