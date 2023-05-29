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
- Masquerade : dd  
- Replay : dd  
- Modification of messages : dd  
- Denial of service (Dos) : dd  

