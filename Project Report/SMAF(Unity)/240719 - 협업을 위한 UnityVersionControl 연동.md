UVC를 활용해서 기존 개발 노트북에 있던 SMAF 데이터를 업로드하고, 다른 컴퓨터에서 pull하여 사용가능한지 확인하였다.
=> 이게 돼야 XR로 협업이 가능하다.
## 정리
필요한 기능 정리
AI - 데이터셋 & AI에 적용
XR 
- 음성의 시작과 끝
- 자막이랑 말풍선 ( 자막은 스마프를 안보고 있을 때, 말풍선은 스마프를 보고 있을 때)
- 메뉴 : 상자 소환(스마프 상자),  
   (상자 소환 위치는 앱 실행 중에는 고정 > 소환 장소 선택, 상자 회수,  )
- 문 열기 어려움 ( 개선 필요 )
- 튜토리얼 (대화형식 & 버튼 주변 반짝 , 처음 시작할 때 뜨고 이후는 튜토리얼 다시 열기 버튼)
- 메뉴에서 터치하면 해당 가방이 떨어짐, 스마프 종류에 따라 가방 앞에 아이콘을 붙임
- 스마프 방에 들어가기 & 스마프를 현실에 소환
   -> 가방을 누르면 스마프가 나옴
   -> 스마프를 누르면 스마프 옆에 메뉴들이 나옴
   -> 스마프 메뉴 
(멀리 있는 경우) 호출하기
(가까이 있는 경우)  얘기하기 & 스마프 방에 들어가기 & 스마프를 방에 돌려보내기 & 스마프 위치 고정하기 & 메뉴 창 닫기
- 스마프 중복 소환 X 
   -> 나와 있는 애 들여보내고 다른 애 나오게 하기
            VS
   -> 디자인 약간씩 다를 경우 스마프 여러 마리 나올 수 있게
   -> 가방에는 가방에 해당하는 스마프만 들여보냄
- 추가 애니메이션( 등장 애니메이션, 문 열릴 때 & 닫힐 때(시야 하얗게) )
- 스마프 던지기 > 스마프 성격마다 다르게 & 친구 스마프는 던지면 좋아하고 선생 스마프는 싫어함

추가 구현
- 간식 주기
간식 역할 : 스마프 위치 이동 & 간식 주기
- 회원가입, 로그인 , 닉네임 입력 받는 것 
- 상자가 앱을 껐다가 키면 상자 사라짐
# 우선 구현할 것들
- 손목에 스마프 상자 소환하기 버튼을 누르면 바닥에 스마프 상자 소환하기 Mode가 되어 원하는 곳에 Pinch하여 상자를 소환할 수 있음.
- 스마프가 돌아다니다가 (SMAF Movement Script On) Ray Point로 클릭하면 호출이 됨.
- 호출 구현 : 호출하면 Random SMAF Movement가 Off가 되고, 새롭게 만든 Player 앞으로 다가오는 Movement Script가 On이 된다. 그러면서 메뉴가 열린다. (질문하기, 방 놀러가기, 위치 고정하기, 집 돌려보내기, 닫기) 닫기를 누르면 다시 Player에게 다가오기 Script가 Off되고, Random SMAF Movement가 On이 되며 메뉴가 닫힌다.