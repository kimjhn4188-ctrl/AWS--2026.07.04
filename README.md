# AWS--2026.07.04
AWS-기초실습 2026.07.04
<img width="2083" height="960" alt="Image" src="https://github.com/user-attachments/assets/da17bf52-8e61-4a3b-bd89-159f01176504" />


A. VPC 생성

B. Subnet 6개 생성 (VPC, Subnet Public, Subnet NAT, Subnet Private 계층 구조와 이중화의 시각화를 위하여)
   Public a, c zone
   Private a, c zone
   NAT a, c zone


C. Internet Gateway 생성


D. NAT Gateway 2개 생성

   -NAT Gateway a -> Subnet NAT a와 연결
   -NAT Gateway c -> Subnet NAT b와 연결


E. Routing table 5개 생성(VPC 기본 Router+ Public Router 1개, Private Router 1개, NAT Router a, c 각 1개)



**NAT Gateway 개념 착각하여 Public 서브넷이 아닌 Nat subnet(Private계층) 에 생성하여 Public Subnet에 다시 생성함.

<img width="1072" height="275" alt="Image" src="https://github.com/user-attachments/assets/1dbbfecb-a731-4244-85fc-e45661f0b05d" />
<img width="1028" height="297" alt="Image" src="https://github.com/user-attachments/assets/f04feca4-4756-41bd-b0d0-421733b434fe" />


1. NAT Gateway vs Load Balancer 차이점
   a. NAT Gateway
   - 아웃바운드(내부서버->외부 인터넷)
   - 단일 공인 IP로 여러 사설 IP를 묶어서 내보냄
   - SNAT 포트(세션 수) 고갈 위험
   
   b. Load Balancer
   - 인바운드(외부 인터넷->내부서버)
   - 여러대의 서버로 트래픽 분산
   - 서버를 늘려서 (Auto Scaling) 트래픽 분산 처리
  
2. NAT Gateway를 어느 서브넷에 생성해야 하는지?

   a. 물리적 생성 위치
   - 반드시 Public subnet에 생성해야함(연결 유형 퍼블릭으로 선택해야함)
   -> NAT Gateway 자신이 IGW와 통신하려면 IGW로 가는 경로가 있는 서브넷이 위치 해야함.
   
   b. 서브넷 제공 대상: Private Subnet 의 VM 들
   - Private Subnet의 라우팅 테이블에서 NAT Gateway로 향하게 설정
     -> 주의: NAT Gateway를 Private Subnet에 만들면, 외부 인터넷과 통신 불가함. 
