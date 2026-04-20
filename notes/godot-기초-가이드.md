---
title: Godot 엔진 한글 기초 가이드
date: 2026-04-20
tags: [godot, tutorial, 한글, game-dev]
---

# Godot 엔진 한글 기초 가이드 (Godot 4 기준)

이 문서는 Godot Engine(주로 4.x 기준)을 처음 접하는 사용자를 위한 간단한 한글 기초 가이드입니다. 공식 문서와 커뮤니티 튜토리얼을 참조해 핵심 개념과 빠른 시작 방법을 정리했습니다. 자세한 내용은 공식 문서를 참고하세요.

출처: https://docs.godotengine.org/ko/4.x/

---

## 1. Godot이란?
Godot은 오픈소스 게임 엔진으로 2D·3D 게임 개발을 지원합니다. 가벼운 실행환경과 직관적인 씬(Scene)/노드(Node) 구조, 자체 스크립트 언어(GDScript)를 제공합니다.

## 2. 설치와 첫 실행
1. https://godotengine.org 에서 최신 Godot 4.x 에디터를 다운로드합니다.
2. 다운로드 후 실행 파일을 그대로 실행하면 프로젝트 매니저 화면이 나타납니다.
3. 새 프로젝트 생성: "New Project" → 경로 지정 → Create & Edit.

## 3. 기본 UI 구성
- 프로젝트 매니저(Project Manager)
- 에디터 상단 툴바: 실행, 디버그 등
- 씬 트리(Scene Tree): 현재 열려 있는 씬과 노드 계층
- 인스펙터(Inspector): 선택한 노드의 속성
- 파일 시스템(FileSystem): 프로젝트 파일 보기

## 4. 씬(Scene)과 노드(Node)
- 씬은 게임의 한 상태를 나타내는 트리 구조입니다(예: 레벨, 캐릭터).
- 노드는 씬을 이루는 구성 요소(예: Sprite, Camera, CollisionShape).
- 씬을 재사용(인스턴스)할 수 있어 계층적 설계가 편리합니다.

예: 2D 플레이어 씬
- Node2D (root)
  - Sprite2D
  - CollisionShape2D
  - Script (GDScript)

## 5. GDScript 기초
- Godot의 기본 스크립트 언어입니다. 파이썬과 유사한 문법을 가집니다.

예제: 간단한 이동 스크립트 (Player.gd)

```gdscript
extends Node2D

@export var speed := 200

func _physics_process(delta):
    var input_vector := Vector2.ZERO
    input_vector.x = Input.get_action_strength("ui_right") - Input.get_action_strength("ui_left")
    input_vector.y = Input.get_action_strength("ui_down") - Input.get_action_strength("ui_up")
    if input_vector.length() > 0:
        input_vector = input_vector.normalized()
        position += input_vector * speed * delta
```

- InputMap에서 "ui_up/down/left/right" 같은 입력 액션을 설정하세요.

## 6. 씬 전환과 신호(Signals)
- 신호(Signals)는 노드 간 통신용 콜백 시스템입니다.
- 버튼 클릭, 충돌 등 이벤트를 신호로 받아 처리할 수 있습니다.

## 7. 물리(Physics)와 충돌
- 2D: RigidBody2D, CharacterBody2D, CollisionShape2D 사용
- 충돌 레이어/마스크로 충돌 대상 설정
- 물리 연산은 _physics_process(delta)에서 처리

## 8. 애셋(Assets)과 리소스 관리
- 에셋 라이브러리나 자체 리소스를 사용
- 이미지, 오디오, 폰트 등을 res:// 경로로 관리

## 9. 디버깅과 출력
- 출력(출력 패널)에서 print() 결과 확인
- 브레이크포인트, 스택 트레이스, 변수 검사 등 제공

## 10. 빌드와 배포
- Project → Export에서 플랫폼별 Export Preset 설정
- 안드로이드/Windows/macOS/Linux 등으로 빌드 가능

## 11. 간단한 2D 예제 워크플로 (요약)
1. 새 2D 씬 생성(Node2D)
2. Sprite2D 추가 → Texture 할당
3. CollisionShape2D 추가 → 모양 지정
4. 스크립트 추가 → 입력 처리 및 움직임 구현
5. 플레이(Play Scene)로 테스트

## 12. 학습 자료(추천)
- 공식 문서(한글): https://docs.godotengine.org/ko/4.x/
- 공식 튜토리얼: Getting Started → Step by Step
- YouTube 튜토리얼(한국어 커뮤니티 강좌)

---

작성자: bot (actioncode-master 요청)
간단 가이드이므로 실제 프로젝트에 적용하기 전 공식 문서의 세부 항목을 반드시 확인하세요.
