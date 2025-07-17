# RPG-Learn

단축키
---
snap -> END키 스냅은 액터를 땅바닥에 붙이는 키

기즈모 위치 변경 -> 마우스 휠 클릭

해당 메시의 디폴트 -> ctrl + e

머테리얼 - 해당 메시에 색깔과 질감을 표현

메시 - 껍데기

피직스 에셋 - 물리적인 효과

스켈레톤 - 움직이는 본

루트 - 스켈레톤의 최상위 본

애니메이션
---
   콘텐츠-캐릭터-플레이어 폴더 만들고 Y-BOT 끌어놓고 스켈레톤-없음 모두 임포트
  
   플레이어-애니메이션-로코 폴더 생성, 모션 FBX 파일을 끌어다 놓고 임포트 옵션에서 스켈레톤을 플레이어 스켈레톤으로 선택
  
   로코 폴더에 우클릭-애니메이션-레거시-블렌드스페이스1D-해당 스켈레톤 선택
  
   애니메이션을 끌어다 놓아 0 1 2으로 설정
  
   애니메이션 폴더에서 우클릭-애니메이션-애니메이션블루프린트-해당 스켈레톤 선택
  
   BP_Player 선택해서 애니메이션에 애닝클래스에 애니메이션블루프린트 선택 -> 애니메이션들 루프로 선택

   움직이는 애니메이션의 경우에는 루트 강제 잠금설정
  
   프로젝트세팅-엔진-입력 축 매핑에 w a s d 추가
  
![image](https://github.com/user-attachments/assets/4446e71a-d6fd-46f6-8afe-3bd1b4be6e42)

  BP_player 이벤트그래프
  
  ![image](https://github.com/user-attachments/assets/73830d78-7730-492d-98eb-046bb25357b5)

애니메이션 몽타주
---
해당 애니메이션 선택-생성-애닝몽타주 생성


플레이어 만들기
---
  플레이어-BP 파일 생성 블루프린트 클래스 생성 -> 캐릭터 더블클릭
  
  스켈레탈 메스 에셋에 Y-Bot 추가, 캡슐과 화살표방향 맞추고 컴파일, 저장
  
  컴포넌트에 추가 - 카메라, 스프링암 -> 카메라암으로 이름 바꾸고 카메라를 카메라암 밑으로 넣기
  
  콘텐츠-레벨-블루프린트클래스 생성 게임모드베이스 더블클릭 디폴트 폰 클래스를 BP_Player로 변경 
  
  프로젝트 세팅에 맵앤 모드에 기본 게임모드를 생성한 게임모드베이스로 변경
  
루트모션 버그수정
---
블랜더의 믹사모 컨버터 마스터를 통해 수정

![image](https://github.com/user-attachments/assets/f71be1b9-9d8c-4d3f-978b-e71eb393d0e3)

버그가 발생하는 이유는 믹사모의 본과 언리얼의 본이 다른경우가 있기 때문.

리타게팅
---
언리얼 엔진으로 캐릭터를 가져올 경우 리타게팅을 통해 애니메이션을 사용할 수 있게 한다.

우클릭-애니메이션-IK 리타게터,IK 릭(베이스),IK 릭(타겟)을 만든다. 

리타게터를 실행시키고 베이스로가서 루트가 아닌 Pevis나 Hips를 리타겟 루트로 설정

spine, neck, leftarm, rightarm, leftleg, rightleg를 체인으로 설정(트위스트는 제외)

입력
---
입력을 받기위해 입력-입력맵컨텍스트

입력액션을 추가 값 타입을 Axix2D로 변경(앞뒤좌우)

IMC컨트롤러에서 매핑을 WSAD는 W (스위즐 입력축값) S (Negate, 스위즐 입력 축 값) A (Negate) D (기본 입력값)

인풋매핑-BP_Player

![image](https://github.com/user-attachments/assets/5424328b-6851-4615-a94c-71a0d2f6dca4)

Move-BP_Player

![image](https://github.com/user-attachments/assets/1fb6c6a6-d291-4dcc-ade6-2c9e6170a48b)

ABP_Player

![image](https://github.com/user-attachments/assets/7d95d3bc-0bcd-48f5-898c-ed1377de6cf3)

걷기(달리기)
---

![image](https://github.com/user-attachments/assets/00736d2c-da6e-49c4-82bd-b0c5fb3ec7b3)

add Movement Input에 사이드 인풋과 포워드 인풋을 받아서 컨트롤 로켕리션을 움직인다.

달리기는 IsRun 변수를 통해 분기를 나눠 X2를 해준다.

Look
---
![image](https://github.com/user-attachments/assets/9aadedc4-a252-4878-b6a5-ad2f18345655)

마우스의 X,Y의 값을 키 매핑으로 받아 마우스가 움직이는 대로 캐릭터가 볼 수 있도록한다.

카메라 범위와 위치
---
![image](https://github.com/user-attachments/assets/7d2b1ec0-14a2-4d2e-ba1f-f8bb1e46c489)

카메라 범위는 마우스 휠, 위치는 방향키로 매핑. IA에서 범위는 1D, 위치는 2D

Jump
---
![image](https://github.com/user-attachments/assets/72fbaf30-1e33-4ada-a997-a9421017e2da)

BP_Player만 아니라 ABP_Player에서의 애니메이션도 추가해줘야 한다. 하지만 점프 애니메이션의 착지 등과 같은 것이 없어서 제대로 구현 못했음.

왼쪽 쉬프트키를 점프키로 키 매핑하고 하면된다.

Crouch
---
![image](https://github.com/user-attachments/assets/e087e8cb-b98b-4e42-853d-cb1b228b6d05)

BP_Player

![image](https://github.com/user-attachments/assets/b816ee10-22b4-4f27-b17d-ae9bc49c5f54)

ABP_Player - 애니메이션까지 설정해야 하기 때문에 ABP까지 건드린다. 

Locomotion에서 Standing_TO_Crouched로 가는방향에는 Is_Crouch를 사용해서 들어가고, Standing_To_Crouched에서 Crouch는 스테이트의 시퀀스플레이어에 체크해준다.

Crouch에서 Crouched_To_Standing으로는 IsCrouch 변수에 NotBool을 사용해서 체크하여 일어서며 Locomotion으로 갈때는 스테이트의 시퀀스 플레이어에 체크한다.

Dodge
---
![image](https://github.com/user-attachments/assets/f34c3b51-e6e2-4720-9883-5a7581e2aaf1)

해당 에니메이션에서 몽타주를 생성해주고 옆으로 움직임이 들어오고 IsDodge 상태가 아니면 닷지를 실행한다. 

사이드 인풋이 0보다 크면 오른쪽, 작으면 왼쪽 움직임. 몽타주 정보에는 메쉬 정보가 필요함.

블랜드 아웃 시, 중단 시에 IsDodge가 False가 되도록 설정하는 이유는 나중에 닷지 시간동안 무적기능을 넣을 때 완료시까지 하게되면 무적시간이 길어지기 때문이다.

중단시는 몽타주 중간에 다른 애니메이션이 덮어써질 경우 회피를 취소해주어야 하기 때문.

몽타주를 실행하기 위해서는 ABP_Player에서 AnimGraph에 Locomotion과 출력 포즈 사이에 몽타주 Defaultslot을 추가해준다.

Lyra 데이터이주
---
콘텐츠 브라우저에서 해당 폴더를 우클릭하고 이주 클릭 - 가져올 파일을 선택해서 이주할 프로젝트의 콘텐츠 선택

가져올려고 하는 애니메이션 데이터의 스켈레톤이 다르면 해당 스켈레톤을 가져와서 리타게팅 진행

Advanced Locomotion
---
시퀀스 매칭이 필요한 변수들 생성

BP_Player의 캐릭터 무브먼트 최대가속과 감속걷기제동을 낮춰준다. 300과 100으로.(수정가능)

애니메이션을 추가하기 전에 애니메이션창에 창-에니메이션 모디파이어를 클릭하고 모디파이어 추가에 DistanceCurveModifier와 SyncMarkerAnimModifier가 없을 경우 언리얼 기본화면에 우측상단 세팅에 플러그인에 모션을 검색하고 AnimationLocomotionLibary, Animation Warping, MotionWarping/을 켜준다.

각각의 Distance 노드를 접근하기위해서 커브 압축세팅을 UniformIndexCurve로 설정해준다.
