---
layout: post
title: "UE4 - BluePrint"
description: ""
date: 2019-05-10 19:00:00+09:00
tags: [ue4]
comments: true
share: true
---

[TOC]



## 설치

- 설치하는데 오래걸린다.
- 프로젝트 생성하고 컴파일 에러난다고 비주얼 스튜디오를 열거냐 물어본다.
- 열었더니 소스 분석만 5분정도 한다.
- 언리얼에서 프로젝트 열었더니 컴파일 안된다고 수동으로 컴파일 하란다.
- 비스에서 빌드하니 15.7버전에서 언리얼 코드 생성에 버그가 있다고 15.9로 업데이트 하란다.



## 액터

- UE4 공간에 배치되어 있는 오브젝트





## 좌표계

- z-up 좌표계
- xy : 평면
  - x : 우 +
  - y : 아래 +
- z : 위
  - z : 위 +
- UE4 좌표계 불일치
  - 월드 뷰포트 좌표계 : Y-front/Z-up
  - 액터의 로컬 뷰포트 좌표계 : X-front/Z-up
  - 따라서 Y-front/Z-up로 임포트한 애셋은 90도 회전되어 나온다.
  - 해결
    - 임포트 시 Y-front/Z-up으로 임포트
    - 블루프린트 또는 프로그램에서 제어하는 애셋은 블루프린트 컴포넌트 Mesh에서 90도 회전
    - 위 방법으로 안되면 임포트 시 오프셋 회전 설정





## 크기

- 단위 cm
- 1유닛 = 1cm





## 에디터 조작

- 뷰포트
  - 게임 스타일
    - MR + z or 1 : 줌인
    - MR + c or 3 : 줌아웃
  - Maya 스타일
    - F : 선택 오브젝트를 중앙에 표시
    - Alt + ML + Drag : 텀블(선택 오브젝트를 중심으로 회전)
    - Alt + MR + Drag : 돌리(선택 오브젝트에 가까워지거나 멀어짐)
    - Alt + MM + Drag : 트래킹(카메라 평행 이동)
  - 2D 뷰
    - MR : 스크롤
    - ML + MR or MM : 줌 인/아웃
  - 액터 옮길 때
    - Alt : 복제하며 옮김
    - Shift : 카메라도 함께 움직임
    - Alt + Shift : 복제와 카메라 이동
  - 몰입 모드 : F11
  - 마키 사용 : ctrl + alt + drag
  - 추천 레이아웃
    - 배치 작업 중심이므로 2분할(상단, 원근) 레이아웃이 좋다.
  - <http://api.unrealengine.com/KOR/Engine/UI/LevelEditor/Viewports/ViewportControls/>
- 블루프린트 에디터
  - ctrl + f : 이벤트 노드 찾기





## 요, 피치, 롤

- (모음의 방향으로 기억한다)
- 요(Yaw)
  - 좌우
- 피치(Pitch)
  - 상하
- 롤(Roll)
  - 바라보는 축(z) 중심으로 회전





## 게임 개발 워크플로(Workflow, 작업 흐름)

- 프로토타입
  - 게임의 재미 검증을 위해 테스트 가능할 정도로 간단히 만들어봄
  - 꼭 디지털일 필요는 없다.
- 프리 프로덕션
  - 게임의 일부분을 완벽하게 만듦
  - 실제 제품 수준으로 만들면서 워크플로를 검증, 개선
  - 버티컬 슬라이스(세로 쪼개기)
    - 스테이지를 쌓아올리고 세로로 잘라서 전체 스테이지에 필요한 기술들을 하나의 스테이지에 모두 구현해본다.
    - 제작의 소요를 산정하기 위한 검증과 기술 축적
    - [http://dnotewiki.com/note/index.php/%EB%B2%84%ED%8B%B0%EC%BB%AC_%EC%8A%AC%EB%9D%BC%EC%9D%B4%EC%8A%A4](http://dnotewiki.com/note/index.php/버티컬_슬라이스)
  - 이 단계에서 만들어진 프로그램, 툴, 파이프라인, 워크플로는 프로덕션 단계까지 이어진다.
  - 현실적 이유로 기술적인 우려가 있는 스테이지만 만들거나, 가장 광범위한 사양이 포함되는 스테이지만 만들 수도 있다.
- 프로덕션
  
  - 본격적인 완제품 제작을 위해 제작체제를 확대한다.





## 워크플로

- 워크플로가 반대로 진행되지 않게 한다.
- 빠른 이터레이션을 할 수 있게 한다.
  - 이터레이션 : 개션할 부분을 찾고 수정하는 과정





## 스테이지 제작 워크플로

- 컨셉 결정

  - 플롯(plot)
    - 스테이지와 줄거리를 구상한다.
  - 컨셉 아트
    - 최종 제품으로 만들기 전에 시각적으로 표현에서 전달하는 것을 목적으로 하는 일러스트의 한 형태

- 플레이 가능한 프로토타입 제작

  - 그레이박스(greybox)
    - 텍스처가 적용되지 않은 직육면체, 원기둥 같은 간단한 메시로 스테이지를 만드는 것.
    - 플레이 방식을 완성한다.
  - 메싱(Meshing)
    - 그레이박스 단계의 임시 메시를 정식 애셋으로 바꾸는 것.
    - 모노코크 방식보다 레고 블록 방식으로 만들어야 교체와 수정이 용이하다.
      - 모노코크 : 배경등을 일체형으로 만드는 것.
    - 그레이박싱 단계에서 블록 단위를 결정해서 작업해야 정식 에셋으로 교체가 쉽다.
    - 참고 : 히어로 애셋
      - 레고 블록처럼 재사용을 목적으로 하지 않고 한 번만 사용하는 것을 목적으로 만들어진 애셋
      - 다른 블록과의 연결과 레귤레이션(regulation)에 얽매이지 않는다.
  - 라이팅
    - 정식 라이트 작업
  - 폴리시(polish)
    - 전체적인 품질 향상
    - 파티클 이펙트, 사운드 배치
  - 워크플로를 반복하며 완성도를 높인다.
  - 제작 단계에서는 최적화에 많을 시간을 쓰지 않는다.
    - 게임의 외형이 어느정도 갖춰진 뒤 최적화를 수행하는 것이 효율적이다.
    - 애셋 제작 단계에서 메시의 폴리곤 카운트(트라이앵글의 수), 뼈의 수, 머티리얼의 스탭 수등의 제한을 두는 정도가 적당하다.






## BSP(Binary Space Patitioning - 이진 공간 분할법)

- 이진 공간 분할법은 하나의 공간을 특정한 최종 목적을 만족할 때까지 공간을 재귀적으로 2개씩 분할하는 과정이다.
- 분할 과정에서 BSP 트리라 불리는 트리 구조가 만들어진다.
- [https://ko.wikipedia.org/wiki/%EC%9D%B4%EC%A7%84_%EA%B3%B5%EA%B0%84_%EB%B6%84%ED%95%A0%EB%B2%95](https://ko.wikipedia.org/wiki/이진_공간_분할법)





## UE4 프로젝트에서 .gitignore

- 다음 파일 폴더만 있으면 프로젝트를 다시 세팅할 수 있다.
  - /Config, /Content, /Intermediate, *.uproject
  - .uproject 우클릭 "Generate Visual Studio project files" 
- .gitignore 파일 만들기
  - <https://www.gitignore.io/>
  - Visual Studio, Unreal Engine을 써넣고 생성
- 참고
  - <https://zenoahn.tistory.com/33>





## 라이팅

- 라이팅 제외
  - 라이트를 두지 않은 상태에서도 뷰포트의 시야를 확보



#### 게임 플레이중 라이트 변경

- F1
  - 와이어 프레임
- F2
  - 라이트 제외
- F3
  - 라이트 포함



## 브러시

- BSP 기능으로 만드는 형상을 브러시라 한다.
- 순서가 있어서 빼기 브러시는 더하기 브러시 다음에 추가되어야 한다.
- 입체성
  - 반입체
    - 불리언 연산이 일어나지 않는다.
    - 빼기 브러시의 영향을 받지 않는다.
    - 빼기 브러시로 깎아 만든 공간에 기둥 또는 장애물을 설치할 때 사용
  - 비입체
    - Collision 판정에 반응하지 않는다.





## 지오메트리 편집

- 브러시 또는 볼륨의 면, 변, 정점을 편집

- 편집

  - 면, 변, 정점을 편집

- 돌출

  - 이동할 때 마다 새로운 면을 추가






## PIE(Play In Editor)

- 선택된 뷰포트
  - 마지막으로 작업했던 뷰포트에서 게임이 플레이된다.
- 새 에디터 창
  - 새로운 에디터 창이 열리면서 게임이 플레이 된다.
  - 화면의 해상도와 화면 비율이 프로젝트에서 설정한 대로 나온다.
- 시뮬레이트
  - 플레이어 캐릭터가 나오지 않고 레벨 공간을 자유롭게 이동 가능하다.





## 이미지 파일 포맷

- TGA/TAGA(True vision advanced raster graphics adapter)
  - 무손실 압축 기반의 비트맵 이미지 파일 포맷
  - 32비트 컬러까지 저장
  - 알파채널 지원
  - 이미지 합성과 영상 편집을 위해 고안
  - 자막 파일이나 동영상 프레임을 '연속된 이미지 파일 시퀀스'로 만들 때 사용
  - 압축률이 안좋아 용량이 큼
  - 호환성이 좋아 윈도우, 리눅스, 매킨토시에서 사용
  - 특허에서 자유로움
- PNG(Portable Network Graphics)
  - 비손실 그래픽 파일 포맷
  - 8비트 알파 채널을 이용한 다양한 투명층 지원
  - 32비트 컬러
  - 알파값이 0인 필셀의 rgb값이 1(흰색) 이다.
    - 이로 인해 유니티에서 png를 불러오면 경계부분에 흰색이 묻어 날 수 있다.
    - 다른 rgb 채널에서 1이하의 값을 넣을 수 있지만 결국 그 컬러가 묻어난다.
    - 해결
      - rgb 채널에서 경계의 색으로 투명한 곳을 채우거나 TGA 파일 포맷을 사용한다.
      - 유니티에서는 텍스처 설정에서 "Alpha Is Transparency"를 체크한다.
      - 얼리얼에서는 자동으로 경계의 색을 확장하므로 이런 문제가 없다.
-  참고
  - <https://itrum.tistory.com/72>
  - <https://ko.wikipedia.org/wiki/PNG>
  - <https://chulin28ho.tistory.com/362>
  - <https://chulin28ho.tistory.com/363>





## FBX 임포트 옵션

- Mesh > Import as Skeletal
  - 뼈대가 없는 fbx를 스켈레탈 메시로 강제 임포트
- Mesh > Auto Generate Collision
  - 콜리전을 자동 생성
- Mesh > Normal Import Method
  - 노멀을 fbx에서 임포트할지 다시 재연산할지를 선택
- Transform > Import Translation
  - 설정한 오프셋만큼 모델의 원점을 이동
- Transform > Import Rotation
  - 좌표계가 다른 DCC에서 만든 모델의 경우 보정해서 임포트한다.
- Transform > Import Uniform Scale
  - 설정한 배율로 모델의 크기를 변경
- Material > Import Materials
  - fbx 데이터를 임포트할 때 머티리얼 정보가 있으면 UE4 머티리얼을 자동으로 생성하고 메시에 적용
- Material > Import Textures
  - fbx에 포함된 텍스처와 같은 경로에 이미지 파일일 있다면 동시에 임포트를 수행





## 스태틱 메시 에디터

- 라이트 이동
  - L + ML + 마우스 이동





## DCC 툴에서 콜리전 추가

- 외부 DCC 툴에서 객체의 이름을 특정 규칙으로 시작하면 UE4에서 콜리전으로 인식한다.
  - UCX_
    - 볼록 형태
  - UBX_
    - 박스 형태
  - USP
    - 구 형태
- 스켈레탈 메시는 외부에서 생성한 콜리전을 가지고 올 수 없고 언리얼 에디터에서 만들어야한다.





## 리디렉터

- 애셋을 이동시고 기존의 경로로 접근해도 새로운 경로로 접근할 수 있게 해주는 기능.
- 처리에 부하가 걸리므로 최종적으로 수정해줘야한다.





## 퍼시스턴스 레벨

- 현재 레벨 에디터에서 읽어 들이고 있는 레벨
- 서브 레벨의 읽기와 언로드를 관리
- 여러 개의 서브 레벨에서 공통으로 사용하는 액터를 배치할 때 사용
- 퍼시스턴스 레발은 언로드 불가, 서브레벨은 언로드 가능





## 레이어

- 폴더처럼 액터를 분류하는 기능
- 하나의 액터를 여러 레이어에 추가할 수 있다.
- 에디터만의 정보
- 게임 중에 레이어로 제어하기는 안됨
- 월드 아웃라이너 패널의 계층 구조에 영향을 주지 않음





## 디버그 카메라

- 게임 플레이 시 게임 카메라를 자유롭게 조작할 수 있는 모드
- `키를 눌러 콘솔 명령 입력 화면이 나오면 ToggleDebugCamera를 입력





## 레벨 블루프린트

- 툴바 > 블루프린트 > 레벨 블루프린트 열기
- Tick 이벤트
  - 각 프레임에서 화면을 새로 그리는 시점 직전에 발생
- 스크립트가 맵과 함께 저장
  - 따라서 스크립트를 재사용하기 힘듦





## 클래스 블루프린트

- 스크립트가 액터와 함께 저장
  - 따라스 스크립트 재사용은 쉽지만, 맵에 있는 액터에 접근이 힘듦





## 블루프린트 에디터

- 내 블루프린트
  - 그래프
    - +버튼을 클릭하여 이벤트 그래프를 추가 할 수 있다.
    - 노드가 많아져 관리가 힘들 경우 새 이벤트 그래프를 추가하여 정리할 수 있다.
      - 새 이벤트 그래프와 기존의 이벤트 그래프는 사실상 연결되어 있다.
- 디테일 패널
  - 그래프
    - 카테고리
      - 해당 변수의 액션 리스트 카테고리를 설정한다.
    - 퓨어
      - <u>순수 함수</u>를 만든다.
        - 입력이 동일하면 결과도 동일한 함수
        - 외부의 데이터를 참조하거나 변경하지 않는 함수
      - UE4에서 순수 함수는 실행 순서를 지정하지 않는 함수
        - 퓨어로 지정해도 외부 변수를 참조할 수 있다.
      - 실행 순서 지정 시 실수를 줄이기 위해 순수 함수로 만들 수 있는 함수는 순수 함수로 만드는 것이 좋다.
  - Physics
    - Simulate Physics
      - 해당 액터에 물리를 적용한다.
  - Collision
    - Generate Overlap Event
      - 오버랩으로 등록해서 충돌시 Overlap 이벤트가 발생하게 한다.
  - 변수
    - 편집가능
      - 블루프린트를 맵에 배치엤을 때 레벨 에디터의 '디테일' 패널에서 값 변경 가능





## 블루프린트 노드

- 연결 끊기
  - Alt + 노드 클릭
- 변수 노드 설치 단축키
  - 변수를 Ctrl 키를 누른 채로 이벤트 그래프 패널에 드래그&드랍하면 get 노드 자동 생성
  - 변수를 Alt 키를 누른 채로 이벤트 그래프 패널에 드래그&드랍하면 set 노드 자동 생성





## 블루프린트 함수 라이브러리

- 여러 블루프린트에서 사용할 수 있는 함수이다.
- 특정한 블루프린트에 종속되지 않는다.
- 특정한 블루프린트의 고유의 요소에 접근하지 않는다.





## 블루프린트 매크로  라이브러리

- 액터 계열 클래스에서 사용하는 GetActorLocation 등의 기능을 사용해서 서브루틴을 만들 경우 사용
- 생성 시 어떤 계열의 클래스의 고유 기능을 사용할지 부모 클래스를 정한다.
- 함수 라이브러리와 같이 공유해서 사용 가능
- 블루프린트에서 독자적인 매크로 생성 가능
  - 이는 해당 블루프린트에서만 사용 가능
- 실행 핑니 필요한 경우 EXEC라는 핀을 추가해서 사용
- 잠재적(지연) 액션을 사용하면 이 매크로는 함수 그래프에서 사용할 수 없다.





## 액터를 움직이는 방법

- 좌료를 매 프레임마타 변경
  - 등속 직선 운동에 적합
- 이동 컴포넌트에 파라미터 전달
  - 관성 등 현실 세계를 반영한 움직임
  - MovementComponent 사용
    - CharacterMovement, RotatingMovement, ProjectileMovement
- 미리 정의한 시퀸서로 이동
  - 키 프레임을 지정하고 특정 시간에서의 위치와 방향을 자동으로 보간하여 움직임
  - 방식
    - 마티네(Matinee)
      - 에디터에서 <u>컷씬</u>을 생성하고 재생하기 위한 구조
        - 컷씬
          - 게임 중간에 3D 모델들이 움직이며 스토리 등을 전달
          - 시네마틱 영상은 동영상을 재생하는 것이므로 컷씬과는 다르다.
    - 타임라인(Timeline)
      - 키 프레임을 사용
- 물리 엔진 이용
  - 게임 오브젝트의 움직임을 물리 엔진이 처리
- 루트 모션 이용
  - 외부 툴에서 만든 애니메이션을 UE4에서 재생



## 액터를 바닥에 붙이기

- end 키
- 액터 우클릭 > 프랜스폼 > 스냅/맞춤 > 바탁에 스냅



## 입력 추출

- UE4 4.10.2 기준으로 게임패드 또는 키 스위치의 상태(현재 눌리고 있는지)를 직접 추출하는 것은 불가능하다.
  - 따라서 오래 누르기, 동시에 누르기, 슬라이드 입력 등은 다루기 힘들다.
- 이런 입력이 필요하면 C++로 하드웨어의 입력 상태를 처리해야한다.





## 입력 매핑

- 가상의 버튼 이름을 설정하고 이에 물리적 키를 매핑하는 방법
- 이식과 사양 변경이 쉽다.
- UE4에서는 프로젝트 세팅에서 설정한다.
  - 툴바 > 세팅 > 프로젝트 세팅 > 엔진 > 입력
- 세팅
  - 액션 매핑
    - 디지털 입력
- 게임패드
  - Xbox One/360 레이아웃을 따른다.
  - 게임패드 전면 아래, 위, 왼쪽, 오른쪽 버튼은 X, Y, A, B버튼을 의미한다.
- 입력 축에서의 Scale 프로퍼티
  - 입력된 값에 곱해주는 값
  - 하드웨어 값 * Scale = 입력된 값
  - 입력을 역전하거나 크기를 조절한다.





## 페르소나 애니메이션 에디터

- 애니메이션과 관련된 작업을 수행할 수 있는 에디터
- 모프 타겟 프리뷰어
  - 얼굴 표정 변화, 차량의 손상 등의 표현에 사용되는 기술





## GameMode, PlayerPawn, PlayerController의 관계

- 조작자를 사람과 AI 중에서 선택할 수 있도록 Pawn은 반드시 Controller 액터로 운용해야한다.
- PlayerController가 하드웨어 입력을 받고 Pawn에 반영하는 것이 정석이지만 작은 게임에서는 불편하므로 Pawn에서도 입력을 받을 수 있다.
- 게임이 시작되면 PlayerPawn, PlayerController가 공간에 존재하며 회전과 관련된 프로퍼티를 가진다.
- Pawn과 Controller의 방향
  - Controller도 액터의 일종이므로 맵에서 위치와 방향을 갖으며 일반적으로 Pawn에 붙어 움직인다.
  - UE4의 캐릭터 방향은 Pawn의 방향을 기반으로 결정
  - 플레이어의 Aiming은 Controller의 방향으로 결정



## 컴포넌트

- 루트 컴포넌트
  - 컴포넌트 계층 구조에서 가장 위에 있는 컴포넌트
  - 액터의 중심점에 위치
  - 다른 자식 계층 컴포넌트 위치의 중심
    - 따라서 루트 컴포넌트는 위치 지정 및 회전 지정이 불가
- Arrow 컴포넌트
  - 화살표를 그려서 액터의 방향을 쉽게 파악하도록 돕는 컴포넌트
  - 에디터에서만 그려진다.





## 블루프린트 이벤트 그래프의 액션 노드

영문에서는 'Game' 카테고리 하나만 있지만 한글에서는 'Game'과 '게임' 두 개가 있고

번역 안된 것은 'Game', 번역 된 것은 '게임'에 들어있다.

다른 액션들도 번역 안된 카테고리와 번역된 카테고리가 공존한다.

- Game
  - OnDestroyed에 이벤트 바인딩
    - OnDestroyed 델리게이트에 실행될 이벤트(함수)를 바인딩 한다.
  - OnDestroyed에 이벤트 할당
    - OnDestroyed 델리게이트에 실행될 Custom Event(함수)를 생성하고 바인딩 한다.
  - Damage
    - Apply Damage
      - Damaged Actor에 할당한 액터에 AnyDamage 이벤트를 호출한다.
  - Get Game Mode
    - GameMode를 가져온다.
- 게임
  - 클래스에서 액터 스폰(SpawnActor from Class)
    - 지정한 클래스(블루프린트)의 액터를 생성하여 레벨에 배치한다.
- Physics
  - Set Simulate Physics
    - 피직스 시뮬레이션을 시작 또는 정지 시킨다
  - Add Impulse
    - 강체에 힘을 가한다.
    - Vel Change
      - 주어진 힘을 그대로 가속도로 사용할지 결정
- Utilities
  - Transformation
    - GetActorTransformation
      - 타겟 액터의 Transform을 제공한다.
    - Get Socket Transform
      - 메쉬 안에 있는 소켓을 반환한다.
      - Transform Space
        - RTS World
          - 월드 위치
        - RTS Actor
          - 액터 상태 위치
        - RTS Component
          - 컴포넌트 상태 위치
  - Time
    - Set Timer by Function Name
      - 지정한 시간 뒤에 지정한 이름의 함수를 실행
  - Flow Control
    - Delay
      - 지정한 시간 후 실행 출력
  - Actor Has Tag
    - 해당 액터가 지정한 태그를 갖고 있는지 여부 반환
  - Array
    - Get
      - 배열의 인덱스에 있는 값을 반환
    - Length
      - 배열의 길이를 반환
  - Name
    - Make Literal Name
      - 스트링 상수를 만든다.
      - 'Make Literal~'로 시작하는 노드
        - 상수를 만들어내는 노드
        - 하나의 상수를 여러 노드에 입력할 경우 사용
- 유틸리티
  - 플로우 콘트롤
    - 시퀀스
      - 일련의 핀을 순서대로 실행
      - 출력이 몇개든 있을 수 있고 순서대로 실행되며 딜레이는 없다.
      - S를 누를 상태로 이벤트 그래프 빈 공간 클릭으로 생성 가능
  - 흐름 제어
    - DoOnce
      - 한 번만 신호를 출력한다.
      - Reset 된 이 후 한 번만 신호를 출력한다.
      - 매크로 노드이므로 더블 클릭으로 구성을 확인해 볼 수 있다.
    - WhileLoop
      - while 문
      - condition이 true이면 Loop Body가 실행, false이면 Completed 실행
    - Gate
      - 열림, 닫힘 상태를 두어 흐름을 제어
- 입력
  - 키보드 이벤트
    - 키보드의 키 입력에 대응하는 이벤트 생성
- Math
  - Boolean
    - AND Boolean
      - And 연산
    - OR Boolean
      - OR 연산
  - Integer
    - Integer + Integer
      - 정수끼리 더한다.
  - Vector
    - Make Vector
      - Vector를 만든다.
- 함수 호출
  - 대상이 갖고 있는 함수를 지정하여 호출한다.
- Break Vector
  - 벡터의 구성 성분을 분리한다. 
  - x, y, z 값을 개별적으로 사용할 수 있다.
- 이벤트 추가
  - AI
    - 이벤트 Receive Execute AI
      - 해당 태스크가 실행될 때 호출되는 이벤트
  - Game
    - Damage
      - AniDamage
        - Apply Damage로 호출된다.
- Collision
  - LineTraceByChannel
    - 직선상으로 레이 캐스트하여 처음 충돌하는 객체를 반환
- Break~
  - 구조체 타입의 내부 정보를 사용할 수 있게 쪼갠다(전개한다).
- AI
  - AI MoveTo
    - AIController를 가진 폰을 특정 위치로 이동시킨다.
  - Run Behavior Tree
    - 비헤이비어 트리를 실행한다.
  - Behavior Tree
    - Finish Execute
      - 태스크의 처리가 끝났을 때 태스크의 성공/실패 여부를 트리에게 알려주는 역할
  - Use Blackboard
    - AI가 블랙보드를 사용하도록 한다.
  - Get Blackboard
    - 블랙보드를 가져온다.
  - Components
    - Blackboard
      - Set Value as Float
        - 블랙보드에 Float로 값을 저장한다.
- Pawn
  - Get Controlled Pawn
    - 컨트롤러가 조작하는 폰을 추출
    - 추출한다.
- Rendering
  - Material
    - Create Dynamic Material Instance
      - Material Instance를 동적으로 생성한다.
      - 생성된 머티리얼을 Mesh의 Materials에 적용한다.
    - Set Vector Parmeter Value
      - 머티리얼의 벡터 파라미터 이름을 지정해서 파라미터 값을 변경한다.
    - Set Scalar Parameter Value
      - 머티리얼의 스칼라 파라미터 이름을 지정해서 파라미터 값을 변경한다.
- Effects
  - Components
    - Particle System
      - Spawn Emitter at Location
        - 지정한 파티클 시스템을 지정한 위치에 지정한 방향으로 이미터를 스폰시킨다.
        - Auto Destroy 핀이 활성화되어 있다면 원샷 파티클 시스템은 자동으로 파괴된다.
- Audio
  - Components
    - Audio
      - Set Integer Parameter
        - In Name으로 지정한 파라미터 값을 설정
        - Audio Switch 노드에 입력값을 전달



#### 순수 형변환으로 변환

- 블루프린트 형변환 노드에서 마우스 우클릭 > 형변환 > 순수 형변환으로 변환 을 클릭 시 형변환 노드에서 실행핀이 제거되어 노드가 보다 유연해진다.





## 블루프린트에 추가한 이벤트 디스패처에 이벤트 바인딩 하기

- 이벤트 디스패처가 있는 블루프린트를 레벨에 배치한다.
- 배치한 액터에서 우클릭 > 이벤트 추가 > [이벤트 디스패처 이름] 을 클릭한다.
- 블루프린트 에디터의 이벤트 그래프 패널이 열리고 이벤트가 추가되어 있다.





## 함수와 이벤트의 차이

- 이벤트
  - Delay와 같이 실행 후 잠시 멈추는 잠재적 액션일 수 있기 때문에 출력 핀을 가질 수 없다.
  - 이벤트 그래프에 배치되어 각각의 이벤트끼리 연결된다.
- 함수
  - 실행 즉시 끝나기 때문에 출력 핀을 가질 수 있다.
  - 독립적인 함수 그래프를 가지며 독립적인 1개의 기능에 집중한다.
  - 함수 그래프에서 이벤트 액션을 사용할 수 없다.
    - 함수는 즉각적으로 실행이 끝나에하는데 이벤트는 즉각 실행 안될 수 있기 때문.
- 둘 다 다른 블루프린트(외부)에서 접근이 가능하다.





## 비헤이비어 트리 노드

- Root
  - 비헤이비어의 시작점
- Sequence
  - 하위 노드를 순서대로 실행
  - 중간에 실행이  실패하면 모두 중단
- Selector
  - 하위 노드중 우선순위가 순서로 조건을 파악하고 조건에 맞는 태스크 하나만 실행하고 종료
  - 하위 노드중 하나라도 성공하면 자신도 성공으로 취급한다.
  - 조건 노드
    - 데코레이터
      - Selector의 조건을 설정
      - UE4에서 14종의 데코레이터를 제공
      - 블랙보드를 기반으로 정보를 교환
      - 추가
        - Selector에서 우클릭 > 데코레이터 추가
      - 데코레이터 노드 종류
        - Blackboard Based Condition
          - 블랙보드에 있는 변수에 대해 조건을 판단한다.
          - 디테일 패널
            - Flow Control
              - 관찰자 중단
                - None
                  - 현재 행동이 종료될 때까지 중단하지 않는다.
                - Lower Priority
                  - 해당 데코레이션보다 우선순위가 낮은 행동(노드)을 중단하고 이 노드를 실행
                  - 중단이 결정되면 중단 대상 태스크에서 [Receive Abort AI] 이벤트 호출
                - Self
                  - 해당 데코레이션이 사용되는 노드의 행동을 중단
            - Blackboard
              - Key Query
                - Is Set
                  - Blackboard Key에 무언가 설정되어있으면(Null이 아니면) 실행
        - TimeLimit
          - 특정 노드 실행 시 특정 시간 이후 강제로 해당 노드를 실패로 만든다.
        - Cooldown
          - 해당 기능을 다시 사용하기 위한 대기 시간
      - 이벤트 그래프
        - 이벤트 추가
          - AI
            - Receive Execution Start AI 이벤트
              - ?
      - 함수
        - PerformConditionCheckAI
          - 행동을 계속할지 판단
- 서비스
  - 주변 정보를 수집하는 센서
  - 직접 행동하지 않는다.
  - 수집한 정보를 블랙보드에 적어 데코레이터와 태스크에게 정보를 전달
  - 디테일 패널
    - 디폴트
      - Service
        - Interval
          - Tick 이벤트의 시간 간격
        - Random Deviation
          - Interval에서 랜덤한 시간을 빼고 더해서 호출 시점을 불규칙하게 만듦
- Task
  - 작은 기능을 가진다.
  - 블루프린트로 만들어진다.
  - 종류
    - Task
      - Move To
        - 블랙보드에 기록되어 있는 벡터 타입의 변수를 사용해 이동시키는 범용 태스크
        - 목표 위치에 도착하면 성공



## 비헤이비어 블랙보드

- 각각의 태스크들이 정보를 적어두고 활용하는 것



## 물리 엔진

- 단점
  - 재현성
    - 같은 입력, 상황이 같은 결과를 보장하지 않는다.
    - 초기화 순서, CPU 부하에 따라 결과가 달라질 수 있다.
  - 제어성
    - 힘과 토크를 가해 물체를 움직일 때 제어하기가 힘들다.
  - 정밀한 시뮬레이션
    - PhysX는 범용 물리 엔진으로 특정 장르에 특화되어 있지 않다.
    - 특정한 게임에 특화된 물리 엔진은 직접 만드는 것이 낫다.





## 피직스 애셋(Physics Asset)

- 스켈레톤의 관절과 관절 사이에 콜리전을 추가해 애니메이션과 함께 움직이게 하는 애니메이션 대응 콜리전.
- 캐릭터 콜리전이 부분적으로 작동해야하는 경우 사용.
- 지형 콜리전과 캐릭터 콜리전을 따로 만든다.
- 컨스트레인트 모드
  - Angular Limits
    - Angular Swing 1Motion
      - 빨간색 원주의 스윙(롤 회전)
    - Angular YMotion
      - 초록색 원주의 스윙(요 회전)
    - Angular Swing 2Motion
      - 파란색 원주의 스윙(피치 회전)



## zero extend

- 작은 크기의 데이터를 큰 크기의 데이터로 변경할 때 데이터가 모자라는 부분을 0으로 채우는 방식





## Physics

#### UE4의 콜리전

- 블록
  - 물리적인 현상이 일어나는 충돌
- 오버랩
  - 물리적인 현상이 일어나지 않는 충돌
  - 단순히 겹치는 것만 검출
  - 트리거
    - 오버랩 활용을 주 목적으로 하는 콜리전
    - 이벤트 박스라고도 한다.



#### 피지컬 머티리얼

- 마찰 등 물리과 관련된 입력값을 갖는 재질(머티리얼)
- 하나의 피지컬 머티리얼은 여러 메시에 적용할 수 있다.
- 피지컬 머티리얼 블루프린트 설정 항목
  - Physical Material
    - Friction
      - 마찰 계수
      - 0에 가까울 수록 마찰이 약해진다.
      - 마찰력
        - 마찰계수 * 질량
    - Friction Combine Mode
      - 두 강체가 접촉했을 때 마찰을 계산하는 방법
      - 방법
        - Average
          - 두 마찰의 평균값. 디폴트
        - Multiply
          - 두 마찰을 곱한다.
          - 마찰은 0~1의 범위로 설정하기 때문에 곱하면 더 작아진다.
            - Physics Material에서 Friction은 0~1 이외의 값도 입력이 가능한데... 
        - Max
          - 두 마찰 중 큰 값 사용
          - 최대한 물리를 멈추고 싶을 때  사용
        - Min
          - 두 마찰 중 작은 값 사용
          - 최대한 물체를 움직이고 싶을 때 사용
      - 여러 머티리얼의 마찰을 어떻게 계산할지 설정
    - Override Friction Combine Mode
      - Friction Combine Mode의 프로젝트 설정을 덮어씀
    - Restitution
      - 회복, 반발계수
      - 0에 가까울 수록 반발력이 약해진다.
      - 1로 설정하면 받은 힘을 그대로 돌려준다는 의미, 1이상은 받은 힘 이상을 돌려준다.
    - Density
      - 밀도
      - 메시 부피와 밀도로 질량을 계산한다.



#### 액터의 피직스 프로퍼티

- Start Awake
  - 체크 시 액터의 스폰(생성)과 동시에 피직스 시뮬레이션이 시작
  - 체크 안하면 해당 액터에 물리적 힘이 가해지기 전까지 피직스 시뮬레이션이 작동하지 않음
- Mass in Kg
  - 액터의 질량
  - 피직컬 머티리얼의 Density와 메시의 부피를 기반으로 자동 계산
  - 체크 시 수동으로 입력 가능
- Enable Gravity
  - 중력 적용 여부
- Center Of Mass Offset
  - 액터의 무게 중심을 수동으로 설정
  - 밀도가 균일하지 않은 메시의 움직임을 만들 수 있음
  - 



## Collision

#### 콜라이더

- 콜리전 형상



#### 객체 채널

- 충돌과 관련된 객체들을 그룹화하고 그룹끼리 충돌할지 안할지를 설정
- 디폴트 채널
  - WorldStatic
    - 스태틱 메시, 브러시, 정적 배경물
  - Pawn
    - 플레이어, AI가 컨트롤하는 게임 캐릭터 Pawn에 사용
  - Vehicle
    - Pawn이 탑승하는 기구
  - PhysicsBody
    - 물리 엔진에게 제어를 맡긴 강체에 사용
  - Destructible
    - 물리 엔진의 기능으로 파괴되는 물체에 사용
    - *[distrΛktəbl]*
      - 파괴할 수 있는
  - WorldDynamic
    - 위 5개에 속하지 못한 것에 사용
    - 모빌리티  설정이 무버블로 되어 있는 스태틱 메시 또는 액터에 사용



###### ObjectType

- 객체 채널을 설정
- 종류
  - 블록(Block, 막음)
    - 콜라이더의 움직임을 막고 서로가 파고들지 않게 한다.
    - 서로에 대해 블록 설정을 해야한다.
      - 그렇지 않으면 무시한다.
    - 서로 블록이면 오버랩 이벤트가 발생하지 않음(?)
  - 오버랩(Overlap, 겹침)
    - 콜라이더끼리 중복을 허용
    - 상태를 검출해서 활용
    - 서로에 대해 오버랩으로 설정
      - Collision > Generate Overlap Events 활성화
  - 무시(Ignore)
    - 서로를 완전히 무시



#### Collision Enabled

- 콜라이더가 콜리전을 가능하게 할지 설정
- 종류
  - No Collision
    - 콜리전 불가
  - Query Only(No Phsics Collision, 물리 콜리전 없음)
    - 쿼리 콜리전(?)만 있고 물리 콜리전이 없음
    - 게임 중에 불필요한 물리 반응을 하지 않음
    - Simulate Physics 설정 시 물리 콜리전이 없으므로 반응하지 않음
  - Physics Only(No Query Collision)
    - 물리 콜리전만 있고 쿼리 콜리전이 없음
  - Collision Enabled(Query and Physics)
    - 콜리전 가능



#### 콜리전 프리셋

- 미리 콜리전 설정을 만들고 적용
- 디폴트 충돌 프리셋은 프로젝트 세팅의 콜리전 페이지에서 가능



#### 사용자 정의 객체 채널과 프리셋

- 프로젝트 세팅 > 엔진 > Collision 에서 설정
- 기본 반응
  - 새 오브젝트 채널 추가 시 설정
  - 기존의 콜리전 프리셋에서 새 채널에 대한 기본 응답 반응을 설정



#### 히트 이벤트

- 콜라이더의 Generate Hit Event 프로퍼티에 체크하면 불록이 충돌하는 프레임에서 OnComponentHit 이벤트가 호출됨



#### OnComponent~와 OnActor~의 차이

- OnActor~
  - 액터가 가진 모든 콜라이더에서 발생한 이벤트에 대해 호출
- OnComponent~
  - 개별 컴포넌트에서 발생한 이벤트에 대해 호출



#### 트레이스 응답(레이 캐스트, 라인 테스트)

- 사용하는 상황들
  - 시야 체크
    - 어떤 지점이 시야에 보이는지 확인
  - 착탄 체크
    - 사격한 순간 레이를 쏴서 명중 판정
  - 차폐 체크
    - 폭발 등의 범위에서 차폐물 등으로 가려졌는지를 판단
- 종류
  - 라인 트레이스
  - 박스 트레이스
  - 스피어 트레이스
- 트레이스 응답과 객체 반응을 따로 설정 가능
- 트레이스 채널
  - 콜라이더에서 트레이스 채널마다 개별적인 응답 설정



## 소켓

- 스켈레탈 메시의 특정 위치에 별도의 뼈를 추가하여 그 위치에 무언가를 얻거나 방출하기 위한 로케이터
- 스켈레톤의 본에서 우클릭하여 소켓 추가 가능





## 패널

#### 월드 세팅

- Kill Z
  - 입력한 수치를 벗어나는 액터를 제거한다.
- 



## 액터를 다른 레벨로 이동

- 월드 아웃라이너에서 액터를 선택
- 레벨 패널로 이동하고 이동하려는 레벨에서 우클릭 > 선택된 액터를 레벨로 이동합니다. 



## 변수

- 블루프린트 에디터에서 변수 복제
  - ctrl + w
- 변수 타입
  - 구조체
    - Blackboard Key Selector
      - 블랙보드의 변수를 선택할 수 있게하는 구조체
      - 비헤이비어 트리와 연결된 블루프린트에서만 사용할 수 있는 특수한 형태의 변수
  - 



## 애니메이션 블루프린트

- 신규 추가 > 애니메이션 > 블렌드 스페이스 1D
  - 범위를 분할하고 분할 위치에 애니메이션 시퀸스를 배치
  - 주어진 파라미터에 가장 가까운 시퀸스 2개를 기반으로 블렌드를 수행
  - 이러한 것을 일반적으로 파라메트릭 블렌드(parametic blend)라 부른다.



## 애니메이션 블루프린트 에디터

- 이벤트 그래프
  - 액션
    - Blueprint Update Animation 이벤트
      - 애니메이션이 변경되는 시점에 호출
- 애님 그래프
  - 액션
    - State Machines
      - State Machine을 추가
- State Machine 노드
  - Conduit
    - 애니메이션을 갖지 않는 노드
    - 조건을 판별하여 트랜지션하고싶을 때 Conduit 노드로 이동하여 판별하고 트랜지션할 수 있다.
- 트랜지션 규칙 그래프
  - 결과 노드의 입력 핀에 True가 입력되면 트랜지션이 수행된다.
  - 액션
    - Asset Player
      - Time Remaining (ratio)(Rabbit_Surprise)
        - 애니메시션의 남은 시간
        - 남은 시간을 1.0~0.0 비율로 나타낸다.
      - Time Remaining
        - 애니메이션의 남은 시간
        - 남은 시간을 초로 나타낸다.
    - 



## 머티리얼



#### 머티리얼 에디터

- 노드 기반의 셰이더 에디터
- 팔레트 노드
  - 텍스처
    - Texture Sample
      - 텍스처에서 색 값을 추출
      - 그래프 영역에서 T + 클릭 으로 생성1
  - 수학
    - Append
      - 두 개의 스칼라 값을 사용하여 Vector2(Float2)를 출력
  - 팔레트
    - ParticleColor
      - 파티클 시스템 에디터(캐스케이드 파티클 에디터)에서 설정한 색상이 출력으로 아옴
      - 머티리얼에 사용하면 색을 변화시킴



#### 머티리얼 에디터 디테일 패널

- Material
  - Opacity Mask Clip Value
    - Blend Mode가 Masked 일 경우 이 수치보다 큰 픽셀은 그리고 작은 픽셀은 그리지 않는다.



#### 머티리얼 도메인

- Surface
  - 표면에 질감이 있는 머티리얼
- Deferred Decal
  - 데칼 머티리얼 
- Light Function
  - 라이트 함수와 함께 사용할 머티리얼
- Post Process
  - 포스트 프로세스 머티리얼



#### 머티리얼 블렌드 모드

- 해당 머티리얼을 렌더링할 때 다른 것들과 어떻게 혼합할지를 결정
- Opaque
  - 불투면 머티리얼
- Masked
  - 머티리얼 입력의 [오파시티 마스크]가 활성
  - 기본적으로 불투명 머티리얼이지만 입력된 마스크 이미지를 기반으로 렌더링하지 않는 부분을 만든다.
  - 알파 합성은 아니다.
- Translucent
  - 반투명 머티리얼
  - 머티리얼 입력의 [오파시티]가 활성화되어 알파 채널 값을 연결
  - 반투명 렌더링은 부하가 크다
    - 특히 디퍼드 렌더링에서 크다
    - 부하를 줄이려면 디어(Dither) 합성등이 있다.
- Additive, Modulate
  - 더하기와 곱하기 합성 블렌드 모드
  - 파티클 시스템 만들 때 사용



#### 머티리얼 셰이딩 모델

- 기본 설정
  - Default  Lit
    - 라이트의 영향을 받는 표준 셰이딩
- Unlit (라이팅 제외)
  - 라이트의 영향을 받지 않는다.
  - 스스로 빛을 내는 물체를 만들 때 사용
  - 이미시브 컬러 정도만 베이스 머티리얼에 전달
- Subsurface (서브서피스)
  - 서브서피스 스캐터링 모델 중에서 가장 빠른 모델 ?
- Preintegrated Skin (사전 통합 피부)
  - 사람 형태 캐릭터의 피부를 셰이딩하는 모델
  - 피부 머티리얼이 목적
- Clear Coat (클리어 코트)
  - 무색의 금속 위에 색이 있는 필름을 입힌 상태를 모델링
  - 반짝이는 자동차의 표면 등을 구현
- Subsurface Profile (서브서피스 프로파일)
  - 피부를 셰이딩하는 모드 중 하나
  - 콘텐츠 브라이저에서 생서한 설정(프로파일)을 사용해 서브서피스 스캐터링 처리를 수행



#### 머티리얼 입력

- 베이스 컬러
  - 해당 머티리얼의 기본색 설정
  - 디퓨즈(Diffuse), 알베도(Albedo)를 이 곳에 연결
- 메탈릭
  - 금속성을 설정
  - 1.0에 가까울수록 하이라이트와 프레넬이 금속에 가깝다.
  - 0.0에 가까울수록 금속성이 없어짐
- 러프니스
  - 머티리얼 표면의 거칠기
  - 1.0 : 거친 ~ 0.0 : 부드러운
  - 거칠면 빛이 산란되므로 하이라이트가 생기지 않고 부드러우면 거울처럼 반사가 된다.
  - 반사 상태를 조절한다.
- 스페큘러
  - 광원을 반사하는 정도
  - 기본적으로 메탈릭과 러프니스로 질감을 설정하고 미세 조정 시 보조적으로 스페큘러 사용을 추천



#### 머티리얼 인스턴스

- 미리 만든 머티리얼을 템플릿을 기반으로 가져와 새로운 머티리얼을 만들 수 있는 기능
- 단점
  - 파라미터가 많아지면 어떻게 변경되는지 파악하기 힘들어진다.
  - 파라미터를 조금만 사용해도 많이 사용하는 것과 차이가 없을 정도로 GPU를 많이 사용한다.



## 텍스처 에디터

#### 텍스처 에디터 디테일 패널

- Compression
  - Compression Settings
    - Masks(no sRGB)
      - 체크 해제하면 색상과 관련된 보정을 하지 않음
      - sRGB(Standard RGB)
        - 디스플레이, 프린터 등의 색상 차이를 막고자 만들어진 색공간의 곡제 표준
        - 베이스 컬러 텍스처는 이러한 색상 보정을 받을 수 있다.
        - 마스크, 노멀 전용 텍스처는 색상 이외의 정보가 포함되므로 sRGB로 색상 보정을 받을 수 없다.
      - 



## 파티클

#### 파티클 에디터

- 캐스케이드 파티클 에디터
- 스프라이트를 방출하는 이미터의 크기는 X축만 의미를 갖는다.
- 파티클은 썸네일을 수동으로 찍어줘야 콘텐츠 브라우저에서 썸네일을 볼 수 있다.



#### 파티클 모듈

- Required
  - 형태, 정렬
- Spawn
  - 생성 양과 빈도
- Location
  - 생성하는 위치
- Lifetime
  - 소멸 시간
- Velocity
  - 방출하는 방향과 속도
- Acceration
  - 방출 후 가속(중력 등)
- Size
  - 초기 크기와 크기 변화
- Color
  - 색 변화



#### 파티클 값을 지정하는 방법을 결정 - Distribution

- Float Constant / Vector Constant
  - 고정값 지정
- Float Uniform / Vector Uniform
  - 최소, 최대 범위 값 지정
- Float Curve / Vector Curve
  - 시간에 따라 변화하는 값 지정



#### 파티클 디테일 패널

- Spawn
  - Rate
    - 1초에 방출할 파티클 양
  - Burst
    - 이미터가 실행되고 특정 시간이 지난 후 원하는 만큼의 파티클을 방출하는 설정
  - 



## 라이트

#### 라이트 프로퍼티

- Light > Intensity
  - 라이트에서 방출되는 에너지의 양
  - 클수록 빛을 받는 부분과 그림자 부분의 명암 차이가 커진다.
- Light > Light Color
  - 라이트의 빛 색상을 지정
  - 라이트 자체에 색이 있는 경우 지정
  - 태양은 약 붉게, 달은 약 푸르게
- Light > Atmospheric Sun Light
  - 디렉셔널 라이트의 방향에 따라 애트머스페릭 포그로 만들어지는 태양의 방향도 함께 변경됨

#### 애트머스페릭 포그

- 대기를 씬에 추가하기 위한 용도
- 대기에 따라 태양 빛이 산란되게 만들어 안개 효과를 냄
- 엔진에서 라이트로 취급하지 않기 때문에 그림자를 만들기 위해서 디렉셔널 라이트 등을 함께 사용해야한다.
- 디렉셔널 라이트의 Atmosphere Sun Light 옵션을 체크하면 태양의 각도를 맞춘다.
  - 체크하지 않으면 Atmosphere for 액터의 방향으로 태양의 방향과 높이가 결정된다.

#### BP_Sky_Sphere

- 언리얼 엔진에서 제공하는 스카이 박스
- Default
  - Refresh Material
    - 링크하려는 디렉셔널 라이트 액터를 움직인 이후에 설정을 머티리얼에 반영시키기 위한 버튼
  - Colors Determined By Sun Position
    - 체크 시 태양의 높이를 기반으로 새벽, 아침, 낮, 노을, 밤 등의 하늘 색을 자동으로 결정
    - 특정한 기상 상태를 표현하고 싶으면 체크해제하고 Override Settings에서 설정한다.
  - Sun Brightness
    - 태양 주변에 발생하는 햇무리. 즉 태양 주의의 동그란 고리를 표현한다.
  - Cloud Speed
    - 구름이 흐르는 속도
  - Cloud Opacity
    - 0이면  구름 없는 맑은 하늘, 수치를 올릴 수록 구름이 많아진다.
  - Stars Brightness
    - 태양의 위치를 낮춰 밤을 만들면 스카이박스가 자동으로 별을 생성
    - 별의 밝기를 Stars Brightness로 조정
- Override Settings
  - Sun Height
    - 디렉셔널 라이트와 링크시키지 않은 경우 Sun Height 프로퍼티를 기반으로 태양의 높이를 설정
    - 태양의 방향은 액터의 요(Yaw) 회전값을 기반으로 설정

#### 라이트매스 임포턴스 볼륨(Lightmass Importance Volume)

- 대역 조명(GI, Global Illumination)
  - 광원으로부터 발생하는 빛의 직접적인 효과와 다른 물체에 반사되어 확산되는 영향까지 계산
  - 사전 준비를 위한 계산량이 많고 실행 중에도 많은 메모리를 소모
  - UE4에서는 대역 조명을 수행할 공간을 제공하고 이 공간안에서만 대역 조명 계산을 수행한다.

#### 리플렉션 캡처

- 조명 반사 결과를 미리 계산해 캐시하고 게임 중에 합성해 반사 효과를 구현

#### 포인트 라이트

- Light
  - Attenuation Radius
    - 빛이 닿는 범위
    - 이 범위까지 빛의 감쇠가 일어남
  - Source Radius
    - 광원 자체의 크기를 지정
  - Source Length
    - 광원이 길이를 가지고 있을 때 사용

#### IES 라이트 프로파일

- 조명 업계에서 조명 기구마다 제공하는 IES(Illuminating Engneering Society)라는 배광 데이터를 이용해서 빛을 정확하게 시뮬레이션 할 수 있다.



#### 라이트 베이크

- 실시간으로 빛과 그림자를 계산하면 부하가 크므로
- 빛과 그림자를 미리 계산하고 라이트 맵 등의 텍스처 이미지로 만들어 사용하는 것



#### 라이트 모빌리티

- 라이트가 정적인지 동적인지 결정
- 스태틱(정적 광원)
  - 라이트의 위치, 방향 등 라이트의 파라미터가 변하지 않는다
  - 베이크된다.
- 스테이셔너리(고정 광원)
  - 위치, 방향을 바꾸지 않는다.
  - 플레이어의 조작에 반응하고 파라미터를 변경할 수 있다.
  - 스태틱보다 무겁고 무버블보다 가볍다.
- 무버블(동적 광원)
  - 위치, 방향을 바꿀 수 있다
  - 빛과 그림자가 동적으로 계산된다.
  - 부하가 크고 품직이 낮다.
- 



## 사운드

- 패닝
  - 리스너를 기준으로 왼쪽에서 발생한 소리는 왼쪽에서 오른쪽에서 발생한 소리는 오른쪽에서 들리는 것
- 감쇠(Attenuation)
  - 가까이에서 발생한 소리는 크게, 멀리서 발생한 소리는 작게 들리는 것
- Spatialize
  - 음원을 3D 공간 좌표에 놓는 것



#### 사운드 큐

- Attenuation
  - 감쇠 
- Spatialize
  - 3D 사운드
- 반경
  - 사운드가 100% 들리는 거리
- Falloff Distance
  - 사운드가 감쇠해서 완전히 안들리는 거리
- Non-Spatialized Radius
  - 이 값보다 가까우는 패닝이 없어진다.
- Attenuate with LPF
  - 감쇠 연산에 로우 패스 필터(고주파수 영역을 자르고, 저주파수 영역만 통과시키는 필터)가 함께 적용
  - 대기 흡수에 의한 감쇠를 모방
- LPFRadius Min
  - LPF 적용이 시작되는 거리
- LPFRadius Max
  - LPF 적용이 끝나는 거리



#### 사운드 노드

- Wave Player
  - 사운드 소스 노드
- Switch
  - 외부에서 입력된 파라미터 값에 따라 여러 개의 입력 사운드 중 하나를 출력
  - 파라미터 언셋은 어떠한 파라미터도 설정하지 않았을 때 출력할 값을 지정



## 무료 에셋

- Infinity Blade
- Soul City



## Words

- prop
  - 소도구
- convex
  - 볼록면의, 볼록한, 볼록면
- pillar
  - 기둥
- hull
  - 겉껍질을 벗기다
  - 겉껍질
  - 덮개
- hull shader
  - 모델의 표면을 삼각형으로 변환
- bonfire
  - 모닥불, 화톳불, 횟불
- IRC(Internet Relay Chat)
  - 실시간 채팅 프로토콜로, 여러 사용자가 대화를 나눌 수 있다.
  - 개인 간의 대화도 가능
  - 'DCC'라는 파일 전송 기능도 제공
- fix up
  - 수리, 개량
- atmosphere
  - 대기, 분위기, 기압
- persistent
  - 지속하는, 끊임없는
- swarm
  - 무리, 떼, 군중
- PoC(Proof of Concept)
  - 컨셉 증명
  - 아이디어를 실체로 만들고, 아이디어가 괜찮은지 따져보는 것
- pawn
  - 저당물, 담보
  - 남에게 이용되는 사람, 남의 앞잡이, (빙의)
    - 언리얼 엔진에선 이 뜻으로 쓰인듯.
  - 사람 또는 AI가 조작하는 것
- marquee
  - 차양, 대형 천막
  - 원하는 영역 선택 툴
- strafing
  - 맹공격하다, 기총 소사, 맹공격
  - 정면을 바라보고 왼쪽, 오른쪽으로 이동
  - 한 지점을 조준한 상태로 이동
- spine
  - 척추
- ankle
  - 발목, 복사뼈
- toe
  - 발가락
- emitter
  -  방사체, 발포자, 발행인
- crouch [krauʧ]
  - 숙이다. 구부리다.
- possess [pəzés]
  - 보유하다, 가지다, 소유하다, 소지하다, 홀리다
- carton [kάːrtn]
  - 카턴, 판지 상자, 판지, 종이 용기, 한 상자분의 용량
- impulse
  - 충동, 충격, 추진력, 자극
- momentary
  - 순간의
  - 끊임없이 되풀이되는, 쉴틈이 없는
- spectator
  - 관중, 관객
- visibility [vìzəbíləti]
  - 눈에 보임, 가시성, 시야
- encounter
  - ~과 만나다, 부닥치다
- property
  - 재산, <u>특성</u>, <u>속성</u>, 부동산, 소유, 토지
- deviation [dìːviéiʃən]
  - 탈선, 일탈, 편차, 이탈
- underlying *[Λndərlàiiŋ]*
  - 기초를 이루는, 근원적인, 기저의
- conduit [kάndwit, -djuːit]
  - (물, 가스 등의)도관, (정보, 물자를 전하는)루트, 파이프.
- locomotion
  - 이동, 운동, 이동력, 보행력
- tint
  - 색조, 엷은 빛깔, 빛깔
- intensity
  - 강도, 강렬함, 집중, 중요성
- lit
  - 불을 밝혔다, 켜졌다, 빛났다, 문학
- unlit
  - 켜져 있지 않은
- translucent
  - 반투명의, 반투명인, 투명한
- emitter
  -  방사체, 발포자, 발행인
- distribution
  - 분배, 배급, 배포, 살포
- burst
  - 터지다, 터뜨리다, 폭발하다, 무너지다,  분출하다.
- look up
  - 올려다보다, 쳐다보다, 검색, 고개를 들다.
- jingle
  - (음악이나 시의) 같은 음의 반복
- spatial
  - 공간의, 공간적인, 장소의
- spatialize
  - 공간 좌표 지정
- 





## 읽어 볼 것

- [FBX 스켈레탈 메시 파이프라인 - Unreal Engine](https://docs.unrealengine.com/latest/KOR/Engine/Content/FBX/SkeletalMeshes/)
- [애니메이션 리타기팅](<http://api.unrealengine.com/KOR/Engine/Animation/AnimationRetargeting/>)
- [애니메이션 리타기팅 (다른 스켈레톤)](<http://api.unrealengine.com/KOR/Engine/Animation/RetargetingDifferentSkeletons/>)





## 참고

- 실전 게임 제작으로 배우는 언리얼 엔진4
- 