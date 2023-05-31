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
Block Cipher은 메세지를 블록단위로 처리하고 encryption, decryption한다. 헤드+내용여러개  
Steam Cipher은 encrypt/decrypt할 때 메세지를 bit나 byte로 처리한다.  
현재의 많은 암호들은 Block Cipher이다.  

plaintext->ciphertext가 될 때 비트or바이트 하나 하나를 암호화하는지, 블럭 단위로 하는지 차이인것이다.  

### 기본적인 사실  
n비트 크기의 plaintext block일 때,
2^n개의 다른 plaintext block이 있다. Reversible mapping의 경우 (암호화가 되면 역함수화 하면 암호해독 = 1:1매칭) 2^n!의 경우의 수를 가진다.  
테이블로 정의되는 key의 길이는 2^n*n비트다. (plaintext block개수*key길이)  
(블럭size가 2비트면, 2^2=4개의 블럭 존재. 키 경우의수는 4!=24가지. 테이블로 정의되는 key길이는 8비트) 블록이 조금만 커도 경우의 수가 매우 커진다.  

### Shannon : Substitution-Permutation Ciphers  
Claude Shannon은 1949년 논문에서 S-P(Substitution-Permutation) 개념을 소개했다.  
S-P 네트워크는 현대 암호학의 기초이다.  
S-P 네트워크는 두개의 원시적 암호화작업을 기반으로 한다. substitution(S-Box)와 permutation(P-Box)  

<b>A 3-round Substitution-Permutation Network</b>
구조를 보면 plaintext가 K0을 XOR하여 S박스 4개에 들어가고 그 값들이 P박스에 들어가서 섞어지면 라운드1. 이후 출력값에 K1키가 XOR되어 S-P박스에 들어가면 라운드2. 이후 출력값에 K2가 XOR되고 마지막라운드3에선 S박스만 통과한뒤 출력값을 K3에 넣어 ciphertext가 된다.  

<b>Feistel Cipher Structure</b>  
Shannon의 S-P Network에선 S-Box가 invertible해야한다(가역적)  
Feistel Cipher 구조에서는 S-box가 invertible할 필요가 없다.  
따라서 Feistel Network는 non-invertible 성분으로부터 invertible구조를 형성하는 방법이다.  
- Encryption : RE16 = LE15 XOR F(RE15, K16)  
- Decryption : RD1 = RE16 XOR F(LE16, K16)  
- RE15 = LE16  
- RD1 = RE16 XOR F(LE16, K16) = LE15 XOR F(RE15, K16) XOR F(LE16, K16) = LE15  
따라서 RD1 = LE15  

<b>A xor 0 = A, A xor A = 0</b>  

Key가 1~n개 있고 여러번 암호화 한 것을 다시 역함수를 거치면 풀린다. non-invertible하지만 전체구성에선 역함수가 가능한 구조.  
라운드 거치며 섞기도, 함수에 넣기도, 그대로 가져오기도하며 점점 암호화가 진행됨  
(그대로 끌고 내려오는 것 반, 섞는것 반. 라운드 거치며 복잡. Inverse존재할필요 X)  
이렇게 F가 non-invertible해도 되기에 디자인하기 편하다.  
Decryption에선 아래서부터 위로 거꾸로 올라가기만 하고 F도 그대로 적용. 순서만 맞으면 됨  

Fiestel Cipher의 설계 요소 : Block size, Key size, Number of rounds (RoundFunction과 연관. 라운드마다 같은 Key쓸지 매 라운드마다 키를 준비할지 라운드별로 Key를 변화시킬지 결정할 것), Subkey generation algorithm, Round function  

### DES (Data Encryption Standard)  
64비트 데이터블록, 56비트 키  
IBM에서 1960년 후반 Horst Feistel이 암호 연구를 시작함.  
이 프로젝트는 1971년 'Lucifer' 암호 개발로 끝이남.  
Lucifer는 64비트 데이터 블록, 128비트 키를 가진 Feistel Block Cipher이다.  
1973년 NBS는 국가암호표준에 대한 제안요청 발행  
IBM은 수정된 루시퍼를 DES로 승인함. (정부가 조금 도움을 주어 바꿔나옴)  
> 설계시에 논란이 있었음.  
Lucifer는 128비트의 키를 가짐. 근데 DES로 바뀌면서 56비트의 키가 됨.  
설계 기준 분류는 S-Box  
NSA(No Search Agency) - 데이터분석부서. 모든 통신을 도감청함  에서 상업용 암호로 재개발된것.

아무튼  
DES는 64비트의 KEY가 들어오고 그 중 56비트가 추려저 사용된다.  
7비트의 정보+1비트의 패리티비트 * 8개 = 56+8 = 64비트  
홀수패리티비트는1, 짝수패리티비트는0.  
(데이터가 바뀌어있으면 짝수개여야하는데 홀수개. => 오류 검증)  

DES는 라운드의 시작과 끝에 Initial permutation 그리고 Inverse Initial permutation이 사용된다.  

예전에는 DES를 공부? = F를 공부하는 것  

64비트의 키에서 패리티비트 8비트 버리기 => Permuted Choice 1 (56비트) => 라운드 넘겨주며 Permuted Choice 2로 8비트 버려서 주고 => 다음 라운드로 가기 전에 Key를 Shift.  
다음 라운드에서도 shift된 56비트를 8비트 버려서 Permuted choice 2하여 Round2에 전달.  
<b>Y = IP^(-1)(X) = IP^(-1)(IP(M))</b>  

DES Round 구조  
32비트의 L, 32비트의 R로 구성되어 있다.  
DES는 Feistel 암호에 대해  
Li = R(i-1)  
Ri = L(i-1) XOR F(R(i-1), Ki)  
1. F는 32비트 R과 48비트의 subkey를 사용한다.  
2. 따라서 F를 48비트로 Expansion(확장) permutation 하고  
3. 그렇게 나온 48비트의 expanded R과 48비트 Key를 XOR 한다.  
4. 그 뒤 8개의 S-box들에 값을 넣어 32비트의 결과를 얻어낸다.  
5. 32비트의 결과를 P-Box에 넣어 Permutation하여 F함수의 결과를 도출한다.  

이후 F함수를 거친 32비트 R(i-1)값은 32비트의 L(i-1)값과 XOR하여 Ri 값이 된다.   

### DES 알고리즘 파악  
- E-Box (Expansion Permutation) : Expansion은 32비트가 입력되면 8행 4열로 만들고, 한 행당 맨앞과 맨뒤에 이어지는 수를 붙여서 만든다. 1번 수 앞엔 32번째 수, 4번 뒤에는 5번 수... 32번 뒤에는 1번 수..  
- P-Box (Permutation Function) : Permutation Table(4x8행렬) 에 index들이 적혀있는데, 입력되는 32비트의 index에서 값을 가져온다.  
- S-Box (Substitution Boxes) : 6bit input to 4bit output 이다. 6비트가 들어오면 0번, 5번비트를 행으로하고 (00, 01, 10, 11 4개의 행을 결정) 1~4번비트를 열로하여 15개의 열로 만든다. 011011은 행이 01, 열이 1101이므로 [1][13]인덱스. 즉 2행 14열이다.  
S-Box는 테이블로 존재한다. 4행 16열로 존재하는 테이블을 매칭해주는 것.    

Round Function F 구조 : R(32)->E->(48) XOR K(48)-> S1~S8 -> (32) -> P -> 32 bits result  

64비트의 Key에서 매 8번째 bit는 무시된다.(패리티비트)  
그렇게 Permuted Choice1은 56비트를 고르게 된다.  
56비트의 Key는 C0와 D0로 28비트씩 이등분한다.  
Key Rotation Schedule 테이블을 사용하여 Key를 개별적으로 1혹은2칸 shift left 한다. (만약 한칸씩 shift left하는 구조라면 28번 라운드 지나면 다시 돌아옴)  
2차 Permuted Choice는 48비트로 Table에 맞게 Permutation하여 뽑아내고, 이후 F함수 내에서 XOR하는 용도로 쓰인다.  

16번의 라운드를 거치면 거의 모든 문자가 다른 결과를 낼 것이다.  

> DES 깨는 방법. 현재는 key가 56비트라 좋은 컴퓨터를 사용하여 Brute-Force하면 깨진다.  
옛날에 (98년) 3억을 들여 DES를 깨는 기계 만들었는데 이 덕에 이틀만에 깨졌다.(EFF's DES-cracker)  
그 이유는 Key가 짧아서. 이제는 안전하지 않다.  
다음 세대의 암호탐색은 AES이다.(현재까지 사용)  

구조를 보고 Feistel구조가 아닌것 아닌것을 예시로 보고 알 수 있어야 한다.  

## 4장  
### Algebra  
수학은 Algebra와 Analysis 두 부류로 나뉜다. 주로 컴퓨터, IT쪽에서 Algebra를 사용한다.  
컴퓨터는 실제 넣을수있는 유효숫자가 얼마 되지 않기에 Real Number를 다룰일이 없다. (표현하기 어려움. 예를들면 파이)  
TCP-IP에서는 데이터를 받았는데 깨지면 다시 보내라고 하지만, 위성통신에선 깨진것을 복구하여 통신  

컴퓨터에서 수를 정확히 나타내려면 일단 Finite(유한)해야한다.  
사칙연산이 가능한 유효숫자를 원함. 위성통신에서도 약간의 오류는 복구할 수 있도록.  

정수도 무한집합인데, 이것을 유한집합으로 만들고 처리.  

### Divisibility  
a=mb 꼴로 둘 수 있다면 a/b가 가능하다고 봄. b|a는 b divides a  
a|1은 a=+-1이고, a|b 이고 b|a이면 a=+-b이다.  
모든 0이 아닌 b는 0을 divides한다.  
a|b이자 b|c이면 a|c이다.  
b|g이고 b|h이면 b|(mg+nh)할 수 있다. (m,n은 임의의 정수)  
a를 n으로 divides하면 a=qn+r, 0 <= r < n , q=내림a/n  
내림이라는건... 내림(11/7)이면 1.xxx이니까 1이되고,  
내림(-11/7)이면 -1.xxx이니까 '내려서' -2가 된다.  
> 코딩에서는 int n = -11/7 하면 -2가 아니라, -1이 나올 것이다.  
표준이 0을 바라보고 가장 가까운 숫자를 택하는 것이 되었기 때문이다.  

연산자 11%7=4가 당연. 근데 -11%7=3이 아니라 -4가 나온다.  
위에서 -11/7=-1로 정의되었기 때문이다. 이론과 프로그래밍의 차이.  

모든 수는 Prime Number(소수)들로 만들 수 있다.  
우리가 컴퓨터에서 사용하는 모든 수는 소수들을 곱하여 만든것이다.  
<b>최대공약수(GCD : Greatest Common Divisor)</b>는  
gcd(a,b) = max[k, such that k|a and k|b]  
gcd(a,b) = gcd(a,-b) = gcd(-a,b) = gcd(-a,-b)  
gcd(60,24) = gcd(60,-24) = 12  

두 정수가 '서로소'하다는 것은 무엇을 의미하느냐,  
두 수의 공약수가 오직 양의 정수 1밖에 존재하지 않다는 것. 예를들어 8과 15  

우리가 수학에서 소인수분해를 하는 방식은 두 수를 두고 공약수로 계속 나누는것! 언제까지? 안나눠질때까지  
<b>근데 숫자가 커질수록 소인수분해는 어렵다.</b>  

gcd를 구하라는 것은 divisor(공약수)을 구하라는 것과 같다.  
너무 수가 크면 어렵다. 따라서 소인수분해가 아닌 다른 방법으로 GCD를 구하는 방법? ==> Euclidean Algorithm  
### Euclidean Algorithm 유클리디안 알고리즘  
d = gcd(a,b)를 찾는 것  
gcd(a,b) = gcd(|a|,|b|) , a>=b>0  
우리는 이러한 조건에서  
a = q1*b + r1 , 0 <= r1 < b 이 된다.  
- 만약 r1=0이면, b|a 이고 d=gcd(a,b)=b가 된다.  
- 만약 r1이 0이 아니면, d|r1 이고 d=gcd(a,b)=gcd(b,r1)이다.  
d|a이고 d|b의 관계는 d|(r1=a-q1*b)라고 할 수 있다.  
c=gcd(b,r1)으로 생각하면,  
d|b와 d|r1 에서 d<=c를 얻을 수 있다.  
c|(a=q1*b+r1)과 c|b 로 우리는 c<=d를 얻을 수 있다.  
따라서 c=d이다. 그래서 gcd(a,b)=gcd(b,r1)이다.  

> 1. ㅇㅇ  
2. ㅇㅇ 
3. ㅇㅇㅇ