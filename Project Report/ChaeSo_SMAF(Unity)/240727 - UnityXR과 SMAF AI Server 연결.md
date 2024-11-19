> AI 서버를 소현이가 Naver Cloud를 사용해서 구현하였다.

#### 서버 주소 환경 변수 지정
- [x] 구현 완료
우선 XR 환경에 적용하기 전에, 코드 내에 서버 IP주소가 그대로 노출되는것이 좋지 않아보였기에 Project폴더에 따로 config.json형태로 저장하여 불러오는 방식으로 구현하였다.
Json으로 불러와야하기에 System.Serializable로 지정한 Class도 만들고 이를 토대로 환경변수 구축도 성공적으로 했다.
#### XR 환경에 음성인식 및 답변 받기 옮기기
- [x] 구현 완료
Test Project에서 마이크 및 서버전송 / 서버에서 받은 답변 자막으로 표시한 프로젝트를 XR에 적용해야 한다. 핵심적인 기능이기에 성공하면 대박
- [x] 문제 해결
PC에서 테스트할 때는 잘 작동하는데 Build만하면 작동하지 않는 문제가 있었다. 처음에는 Android에 있는 권한 문제인가 싶어서 이것저것 많은 시도를 하였는데, Debug를 거치는 과정에서 애초에 서버로 통신이 가지도 않는다는 것을 알게되었다.
알고보니 기존에 녹음한 audioData.wav파일을 www 객체의 SendWebRequest()를 사용하여 파일을 가져온 뒤 byte로 전환했었는데, Local에서 파일을 가져오는 System.IO.File 객체를 활용해서 파일을 가져오니 문제가 말끔히 해결되었다.
#### 상자를 눌러 스마프 소환하기
- [x] 구현 완료
상자를 누르면 스마프가 Instantiate가 된다. 그런데 상자를 없앨때도 같이 없어져야한다. Hierarchy에 있는 Smaf를 없애기위해 GameObject.Find를 통해 소환되어 있는 Smaf를 없앴다.
#### 스마프 위에 말풍선 따라다니기
- [ ] 구현 완료
스마프에게 질문 후 답변을 받을 때 스마프 위에 떠있는 말풍선을 통해 답변받을 수 있음.
Canvas는 Transform이 아닌, RectTransform이라는것을 알고있어야겠다.
아무리해도 따라다니질 않네... 잘 구현하고싶다.

bubbleCanvas = GameObject.Find("SMAF Bubble Canvas");
여기가 문제이다. 나중에 해결하자!