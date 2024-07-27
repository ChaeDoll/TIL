> AI 서버를 소현이가 Naver Cloud를 사용해서 구현하였다.

우선 XR 환경에 적용하기 전에, 코드 내에 서버 IP주소가 그대로 노출되는것이 좋지 않아보였기에 Project폴더에 따로 config.json형태로 저장하여 불러오는 방식으로 구현하였다.
Json으로 불러와야하기에 System.Serializable로 지정한 Cla