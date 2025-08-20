# 데이터 링크 계층 : 랜에서 데이터 전송하기

## LESSION12. 데이터 링크 계층의 역할과 이더넷
### 데이터 링크 계층의 역할
  - 랜에서 데이터를 주고받기 위함
  - 네트워크 장비간에 신호를 주고받는 규칙을 정하는 계층
### 이더넷
  - 랜에서 데이터를 정상적으로 주고받기 위한 규칙
  - 허브와 같은 장비에 연결된 컴퓨터와 데이터를 주고 받을 때 사용
    - 허브는 컴퓨터가 동시에 데이터를 보내면 **충돌**(collision)이 발생한다
  - 여러 컴퓨터가 동시에 데이터를 전송해도 충돌이 일어나지 않는 구조 = 데이터를 보내는 시점을 늦춘다 = CSMA/CD방식 사용
  - **CSMA/CD**(Carrier Sense Multiple Access with Collision Detection)
    ![CSMA/CD](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FzGwUv%2FbtrgC6jIcjF%2Fyx5NLssLBz9pNKpazjf2Mk%2Fimg.png)
    - CS : 데이터를 보내려고 하는 컴퓨터가 케이블에 신호가 흐르고 있는지 아닌지를 확인한다.
    - MA : 케이블에 데이터가 흐르고 있지 않다면 데이터를 보내도 좋다.
    - CD : 충돌이 발생하고 있는지를 확인한다
  - 이더넷 헤더를 이용한 통신 흐름
    - 데이터 전송  
    ![데이터 전송](https://velog.velcdn.com/images/sunnamgung8/post/f094e698-7328-4683-b270-fbb2ff66790d/image.png)
      - 보내는 측의 컴퓨터에서 캡슐화 발생
      - 데이터 링크 계층 : 데이터에 이더넷 헤더&트레일러를 추가하여 프레임을 만듬 = 캡슐화!
      - 물리 계층 : 프레임 비트열을 전기 신호로 변환하여 네트워크를 통해 전송
    - 데이터 수신  
    ![데이터 수신](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FlA7nr%2FbtrgAKWxD0b%2FCckE4GbgTinrEiWbMe29f0%2Fimg.png)
      - 해당 포트로 수신하고 나머지 포트로 데이터 모두 전송
      - 데이터를 받는 컴퓨터 측에서 자신의 MAC주소와 목적지 MAC주소를 비교하여 다르면 데이터를 파기하고, 동일하면 데이터 수신
      - 물리 계층 : 전기 신호 > 비트열 데이터로 변환
      - 데이터 링크 계층 : 이더넷 헤더&트레일러 분리 = 역캡슐화!
    - 컴퓨터 2대 이상 동시에 데이터를 전송하는 경우엔 CSMA/CD 방식 사용
## LESSION13. MAC주소의 구조
### MAC주소
- Media Access Control Address(물리 주소)
- 랜카드에 전 세계에서 유리한 번호로 할당됨
- 48bit숫자로 구성 : 앞/뒤 24bit  
  ![MAC주소 구성](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FQOhFY%2FbtrgA7c7h6E%2F1tOWoPT51CbL26vSeKGd7k%2Fimg.png)
### 프레임(frame)
- **이더넷 헤더** : 14byte  
    ![이더넷 헤더](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FCWLs3%2FbtrgIPaf40x%2F3cyTdFTFPNWLpUwEzhqxNK%2Fimg.png)
  - 목적지 MAC주소(6byte), 출발지 MAC주소(6byte), 유형(2byte)
  - 이더넷 유형 : 이더넷으로 전송되는 상위 계층 프로토콜의 종류
    - 0800(IPv4), 0806(ARP), 8035(RARP), 814C(SNMP over Ethernet), 86DD(IPv6)
- **트레일러** = FCS(Frame Check Sequence)
  - 데이터 전송도중 오류 발생하는지 확인하는 용도
    
## LESSION14. 스위치의 구조
### 스위치(switch)
  - 레이어 2 스위치 or 스위칭 허브
  - 스위치에는 **MAC 주소 테이블**이 존재
    - 스위치의 **포트 번호**와 해당 포트에 연결되어 있는 컴퓨터의 **MAC주소**가 등록되는 데이터베이스
  - 스위치 전원 켠 상태 = MAC주소 테이블에 아무것도 등록되지 않은 상태
  - **MAC 주소 학습 기능** = **프레임**이라는 데이터가 전송되면 MAC주소 테이블을 확인하여 출발지 주소가 등록되어있지 않으면 MAC주소를 포트와 함께 등록한다.
  - 목적지 주소가 MAC 주소 테이블에 미등록?  
    ![플러딩](https://velog.velcdn.com/images%2Fkimmainsain%2Fpost%2F49a665dd-b0cb-4398-9026-fa0e65b5531c%2FKakaoTalk_20220307_154233509_02.jpg)
    - **플러딩(flooding)** = 수신 포트 이외의 모든 포트에서 데이터를 송신하는 것
  - 목적지 주소가 MAC 주소 테이블에 등록  
    ![MAC 주소 필터링](https://velog.velcdn.com/images/sunnamgung8/post/dad4abe3-4519-42c7-a237-fc3f53ef9a1a/image.png)
    - **MAC 주소 필터링** = MAC주소를 기준으로 목적지를 선택하는 것
    - 목적지 컴퓨터에만 데이터가 전송됨

## LESSION15. 데이터가 케이블에서 충돌하지 않는 구조
### 통신 방식
#### 전이중 통신 방식
![직접 랜 연결](https://velog.velcdn.com/images%2Fkimmainsain%2Fpost%2F5052f1f7-7015-46e7-ad5b-3432be018415%2FKakaoTalk_20220307_161419138.jpg)
![스위치 연결](https://velog.velcdn.com/images%2Fkimmainsain%2Fpost%2F2aa56fd7-e947-4c25-a78f-d6c477e5f37d%2FKakaoTalk_20220307_161419138_02.jpg)
  - 데이터의 송수신을 동시에 통신하는 방식
  - 데이터를 동시에 전송해도 충돌이 발생하지 않음
  - 컴퓨터 간 직접 랜 케이블로 연결하거나 스위치로 연결하는 방식
#### 반이중 통신 방식
![허브 연결](https://velog.velcdn.com/images%2Fkimmainsain%2Fpost%2F32657f59-00d1-4a35-83cd-59f1629edff4%2FKakaoTalk_20220307_161419138_01.jpg)
  - 회선 하나로 송신과 수신을 번갈아가면서 통신하는 방식
  - 데이터 동시 전송 시, 충돌 발생
  - 허브 사용하여 컴퓨터를 연결하는 방식

### 충돌 도메인
  - 충돌이 발생할 때, 그 영향이 미치는 범위
    - 허브의 충돌 도메인 : 연결되어 있는 컴퓨터 전체
    - 스위치의 충돌 도메인 : 허브보다 좁다
  - 충돌 도메인 범위가 넓을수록 네트워크가 지연된다.

> ARP(Address Resolution Protocol)
> 목적지 컴퓨터의 IP주소를 이용하여 MAC주소를 찾기 위한 프로토콜

## LESSION16. 이더넷의 종류와 특징
### 이더넷 규격
  ![주요 이더넷 규격](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FrkumM%2FbtrgA6k27US%2FdNOXNeeKdAWweCWV3F2pKK%2Fimg.png)
  - 케이블 종류, 통신 속도에 따라 다양한 규격으로 분류  
    ![규격 뜻](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FddiMNh%2FbtrgDVbfxGv%2FpX4sPtKWNXVfGltXiLsImK%2Fimg.png)
    - 하이픈 뒤 : 케이블 길이 or 케이블 종류
      ex. 동축케이블은 최대 길이를 100m단위로 표시
