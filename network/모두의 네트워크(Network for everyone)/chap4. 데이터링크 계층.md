# 데이터 링크 계층 : 랜에서 데이터 전송하기

## LESSION12. 데이터 링크 계층의 역할과 이더넷
### 데이터 링크 계층의 역할
  - 랜에서 데이터를 주고받기 위함
  - 네트워크 장비간에 신호를 주고받는 규칙을 정하는 계층
### 이더넷

## LESSION13. MAC주소의 구조
### MAC주소


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
