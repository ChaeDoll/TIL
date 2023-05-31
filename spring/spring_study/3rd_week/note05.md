섹션5 - 회원가입 예제, 웹 MVC  

회원 가입하는 예제를 실습하여 만들기 시작했다.  
기본적으로 서버를 열면 localhost:8080/ 이 열린다. 그렇기에 home화면을 띄우기 위해 먼저 홈컨트롤러를 생성하고, @GetMapping을 ("/")으로 설정하여 기본적으로 localhost:8080에 진입하였을 때 띄울 창을 설정한다. 매핑된 메소드 안에 "home"으로 반환하면, 먼저 우선순위로 템플릿에 home이라는 html양식이 있는지 찾고 없으면 정적 페이지에 home.html이 있는지 찾을 것이다.  
우리는 템플릿에 home 양식을 만들어 놓았기에 그 양식에 맞게 화면이 출력된 것을 볼 수 있다.  

홈화면을 띄웠으면, 이제 회원을 등록하는 방식이 필요하다. 회원을 관리할 MemberController를 생성한 뒤, 그곳에 회원가입 창과 회원목록 창을 Getmapping하여 사이트 양식을 불러오도록 만든다.  

회원가입의 경우에 html의 form기능을 사용하여 input으로 입력받은 값이 다시 MemberController로 post방식과 함께 반환되도록 설정하고, MemberController에 @PostMapping 기능을 사용하여 post방식으로 반환된 값을 레포지터리에 저장할 수 있도록 한다. (PostMapping에 아까 반환된 form값을 사용하여 new Member를 만들고 member.setName("form.getName()")으로 입력받은 값을 이름으로 하는 멤버 생성) 이후 멤버서비스에 멤버를 가입시키면 회원가입이 정상적으로 진행된 것이다.  
모든 과정을 거치고 나서 "redirect:/"으로 반환하면 이전 홈 화면으로 복귀하게 된다.  

회원조회에서 thymeleaf기능이 주로 사용되는데, members에 저장되어 있는 ID들을 하나씩 불러와 ID와 이름값을 반환하여 화면에 출력해준다.  

현재 우리가 만들고 있는 실습은 Memory를 사용한 Repository를 이용하고 있다. 따로 데이터베이스가 존재하는 것이 아니기 때문에, 서버를 종료하면 당연히 메모리가 종료되고, 기존에 저장되었던 값들 또한 초기화가 된다. 우리가 값이 저장되는 데이터베이스가 필요한 이유가 바로 이것이다.