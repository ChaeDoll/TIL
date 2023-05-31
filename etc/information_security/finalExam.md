# 정보보안 기말고사 공부  
## 0장  
### 현대 암호학의 선구자들  
정보보안의 아버지 <b>Claude Elwood Shannon</b>
암호학에 새로운 방향성을 제시한 <b>W.Diffie and M.Hellman</b>  
전자서명을 위한 방법과 Public-Key 암호시스템을 개발한 <b>R.Rivest, A.Shamir, L.Adleman</b>  

과거에 암호는 군용기술이었다.  
암호는 개인이 공부하지 못하였고, 따라서 암호연구는 몰래 숨어서 했다.  

## 1장  
컴퓨터 보안이란  
정보 시스템 자원에 대한 무결성, 가용성, 기밀성 유지와 같은(CIA) 목적 달성을 위해 자동화된 정보시스템에 적용되는 보호  

### CIA triad (보안 3요소)  
- Confidentiality (기밀성) : 메세지를 숨기는 것. 인증된 권한이 있는 사람은 읽을 수 있고 권한 없는 자는 읽을 수 없음  
- Integrity (무결성) : 데이터가 위변조 되지 않도록 하는 것.  
- Availability (가용성) : 시스템이 항상 안정적으로 유지될 수 있는 것. 항상 사용가능하게 동작하도록 하는 것.  
- 추가적으로... Authenticity (인증된), Accountability (뚫렸을 때 누구의 책임인가.. 책임추궁) 등  

### 보안 공격 (Security Attacks)  
보안 공격에는 Passive attacks(수동적/소극적 공격)과 Active attacks(능동적/적극적 공격)이 있다.  
보안에서는 기본적으로 통신채널이 언제든 도청 당할 수 있음을 가정한다.  
수동적 공격은 메세지를 보는 것이고, 능동적은 메세지를 수정하는 등 직접적인 영향을 주는 것  

수동적 공격은 직접적으로는 큰 영향은 주지 않지만 (공격의 심각성은 낮음) 공격대상자가 알아차리기 어렵다. 도청이 그 예시  
능동적 공격은 직접적으로 영향을 주는 대신, 공격이 일어났는지 감지되는 경우가 많다. 값을 위변조하는게 예시  

<b>수동적 공격</b>  
- Release of message contents : 중간에 도청하여 메세지 내용을 보는 공격  
- Traffic analysis (트래픽 분석) : 암호를 걸어서 메세지를 볼 수 없더라 해도, 네트워크 통신을 주고 받은 빈도수 혹은 누구와 통신을 했는지 등 트래픽 분석으로도 유의미한 정보를 습득할 수 있다.  

<b>능동적 공격</b>  
- Masquerade : 송신자를 Fake 치는 것. 마치 Bob이 송신한것처럼 보이지만 사실은 Darth가 보낸 메세지. 수신자에게 혼동을 줄 수 있다.  
- Replay : 요청을 다시 보내는 공격이다. 예를들면 송금 요청을 보내면 그 유효메세지를 그대로 다시 보내는 것  
- Modification of messages : 송신자가 수신자에게 메세지를 보내면 중간에 빼돌려서 메세지를 복제하여 수신자에게 보내는 것.  
- Denial of service (Dos) : 서버를 망치는 공격. 물리적으로 부수거나, 서버 관리자를 매수하거나 등이 있지만 실질적으로 쓰이는 DoS공격은 '강제로 트래픽을 증가시켜 과부화가 오도록 하는 것'을 주로 말한다.  
DoS공격을 위해서는 디바이스 수가 많아야한다. 그래야 구별이 어렵기때문. 요즘에는 DDoS공격을 주로 한다. (Distributed DoS)  
트래픽 증가를 위해 10만대의 컴퓨터를 쓰는 것보다는 관리자 매수가 빠를텐데, 그래서 바이러스를 사용하여 여러 컴퓨터들을 DoS를 위한 디바이스로 사용한다.  


보안서비스는  
Authentication(아이디 비밀번호로 확인하는 등), Acces control(접근을 통제. 집의 현관문), Data confidentiality, Data integrity, Non-repudiation(부인방지 부인봉쇄 시스템. 이걸위해 전자서명을 함)..  

## 2장  
### 대칭키암호(Symmetric Encryption)  
conventional, secret-key, single-key encryption으로도 불림  
1970년 public-key encryption이 나오기까지 유일한 암호체계였다.  
두가지 유형 암호화 중 가장 널리 사용되는 암호화  
송신자와 수신자는 공통키를 공유한다.  
모든 classical encryption algorithms는 symmetric이다.  

기본용어(Basic Terminology)  
plaintext, ciphertext, cipher, key, encrypt, decrypt, cryptography (암호화 원리와 방법을 연구하는 자), cryptanalysis (키를 모른 채 암호문을 해독하는 원리와 방법을 연구하는 자. codebreaking), cryptology (암호학 및 암호분석 분야)  

대칭키 암호는 plaintext를 key를 사용하여 encryption algorithm으로 넣고 전송한뒤, 똑같은 key를 사용하여 decryption algorithm을 사용하면 다시 plaintext가 됨.  

보통 Symmetric Cipher Model은 message X를 Key를 기반으로 Encryption하고, Y=E(K,X)로 Destination에 송신한다.  
하지만 통신이 이루어지는 Y의 경우를 안전하지 않다고 가정한다. Cryptanalyst는 이 Y를 빼돌려서 K와 X를 유추한다.  
Key는 Secure Channel에 의해 Destination쪽에 보내지는데,  
통신으로 받은 Y를 Secure로 받은 K를 통해 Decryption하여 Message를 수신한다.  

### Kerckhoffs의 원리  
암호화 방법은 꼭 비밀일 필요는 없다. 언제나 적들에게 알려질 수 있다. 오히려 공개되어 있어야 한다?  
그러면 결국, 'Key'에만 의존하는 암호방식을 사용해야한다. key는 적에게 노출되지 않음  
알고리즘 공개 장점 : cryptanalysis가 깨기 위해 노력하고 그 정보를 통해 더 강화된 암호 가능  

- Cryptanalytic attacks (암호분석식 공격)  
ciphertext-only attack : 암호문만 보고 원문을 알려하는 것  
known-plaintext attack : 원문 예시들을 우연하게 좀 알고나서 암호를 해독하는 것  
chosen-palintext attack : 원하는 원문을 넣어보며 암호를 공부하고 해독하는 것  
chosen-ciphertext attack : 원하는 암호문을 해독 알고리즘에 넣어보며 이를 공부하고 공격하는 것    
- Brute-force attack (무식한 문제 해결)  

### 암호 종류 - Classical Substitution Ciphers  
- Caesar cipher / shift cipher  
- Monoalphabetic ciphers  
- Polyalphabetic ciphers / Vigenere cipher  
- One-time pad  

<b>Caesar cipher</b>은 shift cipher의 기초이다. 3개씩 문자를 뒤로 밀어서 출력하는 알고리즘  
a부터z까지 0~25의 숫자로 1:1 매칭을 시킨다.  
그리고 Encryption을 할 때 Key값(3)을 원문숫자에 더하여 ciphertext로 바꾼다.  
식으로 정리하면  
c = E(3,p) = (p+3) mod 26  
p = D(3,c) = (c-3) mod 26  
예를 들어 e(4)값을 넣으면 4+3=7이라 h가 나온다.  
<b>Shift cipher</b>은 언제나 3개씩 뒤로 미는 Caesar cipher를 보완한 방법이다.  
Caesar cipher은 언제나 똑같은 방법으로 밀었기에 Key가 없었다. shift cipher은 방법은 똑같지만 Key를 통해 미는 양을 정한다.  
c = E(k,p) = (p+k) mod 26  
p = D(k,c) = (c-k) mod 26  
> 하지만 1번~26번 미는 bruteforce 방식으로 충분히 쉽게 파훼할 수 있다.  
밀다보면 원문이 나오기때문이다.  
문제는 KeySpace(범위)가 26밖에 안된다는 점이다. 더욱 큰 것이 필요  


<b>Monoalphabetic Ciphers</b>는 a~z를 순차적으로 밀지 않고, 랜덤하여 숫자를 배정한다.  
이렇게되면 key의 가지수가 26!(26팩토리얼)만큼 나온다. 약 2^88로 BruteForce가 불가능하다. 하지만 경우의 수를 제거하다보면 조금은 쉬워진다.  
> 원문을 바로 알 수는 없지만 같은 알파벳이 몇번 쓰이는지는 알 수 있을 것이다.  
이 말은 즉슨, 정보가 많이 들어오면 올수록 자주 쓰이는 알파벳을 분석하여 원문의 방식을 유추할 수 있게 된다.  
잘 안나오는 문자는 q,x,z같은 문자이고, 빈도수가 잦은 문자는 e,i 같은 것이 있다.  
결국 대입을 잘 하다보면 유추가 가능해진다.  
Frequency Analysis라는 영단어 알파벳 빈도수 분석 자료를 사용하여 정보가 길어질 수록 저 자료와 유사해질것이고, 이렇게 대입하여 풀다보면 풀 수 있게 된다.  
t뒤에x는 없고 q뒤에u, t뒤에h 처럼 자주 나오는 규칙도 있으니.. 아무튼 긴 문장에서만 가능하겠지만 이런 유추가 가능해진다.  
통계로 해결되지 않기 위해선 여러번 등장한 알파벳이 같은 알파벳일수도, 아닐수도 있어야함. 따라서 Frequency Analysis가 평평하도록 만들어지게...  

<b>Polyalphabetic Cipher</b>  
암호문에서 알파벳들의 분포가 Flat하도록 설계하는 방법이다.  

<b>Vigenere Cipher</b>  
shift cipher의 반복. 자릿수마다 키를 다르게하여 key+plaintext=ciphertext 방식으로 함.  
예를 들어 key를 LEMON으로 두면,  
KEY : LEMONLEMONLE...  
PLA : ATTACKTODAWN  
CIP : LXFOPVEFRNHR  
plaintext가 a~z를 0~25로 나타냈듯이, key도 똑같이 0~25로 나타내고 key와 plaintext를 1:1로 더해주어 ciphertext를 출력한다.  
> Kasiski's method로 파훼되었다.  
반복되는것을 찾았다. Key의 자릿수가 9자리 수라면 우연히 단어가 겹치는 것은 9또는 3의 배수마다 단어 겹침이 이루어 질 것이다.  

Vigenere Cipher의 강화법은 Key를 메세지만큼 길게 사용하는 것이다.  
<b>One-Time Pad</b>  
위 Vigenere Cipher의 강화법을 사용한 것이 바로 OneTimePad이다.  
메세지 길이만큼의 Random Key를 갖는 암호로 a~z까지의 0~25의 수, 그리고 여백(26)까지 key로 사용한다.  
> One-Time Pad는 완전암호를 만족한다! 절대 깨지 못한다는 안정성을 가진다.  
현재까지도 깨지 못하는 방식이다. 하지만 사용하지 않는 이유가 있다.  
메세지와 키가 똑같은 길이는 갖는다는 것은 그만큼 key의 용량이 매우 크다는 것.  
안전하지만 용량때문에 사용이 불편하고 어렵다.  

이처럼 key의 길이가 메세지 길이만큼 길면 완전암호를 만족할 수 있는 것을 알았다.  
현대암호는 이러한 점도 중요하지만 '쓰기 쉬운' 암호 또한 중요하다고 여기고 있다.  

### Transposition Cipher  
암호는 심볼대체, 위치변경 두가지 방법밖에 없다.  
위에서 알아본 Caesar, Shift, Monoalphabetic, Polyalphabetic, Vegenere, One-Time Pad는 모두 심볼대체 Cipher이다.  

위치변경(Transposition) Cipher는 무엇이냐,  
말 그대로 위치를 바꾸어주는 것이다.  
- Rail fence cipher  
meet me after the toga party를  
m e m a t r h t g p r y  
 e t e f e t e o a a t  
=> mematrhtgpryetefeteoaat  
이렇게 만드는 방법.  
- Columnar transposition cipher  
문장을 원하는 길이 단위로 잘라서 열로 만들고,  
attack postponed until two am  
라는 문장을 예를들어 7개의 알파벳씩 잘라서 7개의 열로 이루어진 행렬로 만들고,  
1 2 3 4 5 6 7의 열 순서로 이루어진 문장을 key로 4 3 1 2 5 6 7 처럼 랜덤하게 둔뒤 1번 열에 있는 알파벳들-> 2번 열에 있는 알파벳들 -> 3번 열... 이렇게 쭉 나열하는 것이다. 위 문장을 예시로 들면  
attackp  
ostpone  
duntilt  
woamxyz  
가 될 것이고, key가 4312567 이라면  
ciphertext : ttnaaptmtsuoaodwcoixknlypetz 이다.  


암호 보안성 면에서 보았을 때,  
substitutions와 transpositions의 방식은 언어의 특성 때문에 그리 안전하지 않다.  
그래서 암호방식을 여러번 사용하여 더욱 안전하게 만든다.  
substitution을 2번 쓰는 것 혹은 transposition을 2번 쓰는 것 보다,  
substitution과 transposition을 섞어서 사용하는 것이 훨씬 안전한 암호를 만드는 방법이다.  
<b>이것이 classical에서 modern 암호학으로 넘어가는 다리 역할</b>  

### Steganography (암호화의 대안)  
alternative to encryption인데..  
메세지 존재 자체를 숨기는것.  
보이지 않는 잉크를 쓰거나, 그래픽 이미지나 사운드 파일에 숨기거나..  
encryption의 사용을 모호하게 할 수 있다는 장점이 있지만 비교적 작은 양의 정보를 숨기기 위해 훨 큰 데이터가 필요.  


## 3장  
Modern Block Ciphers (현대 블럭 암호)  
의 디자인 원리에 관해서 알아본다.  
그 중에서 DES(Data Encryption Standard)에 대해 알아볼 예정.  

Block Cipher과 Stream Cipher가 있는데,  
Block Cipher은 메세지를 블록단위로 처리하고 encryption, decryption한다.  
Steam Cipher은 encrypt/decrypt할 때 메세지를 bit나 byte로 처리한다.  
현재의 많은 암호들은 Block Cipher이다.  

plaintext->ciphertext가 될 때 비트 하나 하나를 암호화하는지, 블럭 단위로 하는지 차이인것이다.  

### 기본적인 사실  
n비트 크기의 plaintext block일 때,
2^n개의 다른 plaintext block이 있다. Reversible mapping의 경우 (암호화가 되면 역함수화 하면 암호해독 = 1:1매칭) 2^n!의 경우의 수를 가진다.  
테이블로 정의되는 key의 길이는 2^n*n비트다.  
