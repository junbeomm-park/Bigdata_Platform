# Linux

> VMware 설치

1. Vmware.exe 실행

2. 가상키보드 체크

3. 환경개선 모두 체크해제

4. Play -> new virtual machine 클릭

5. OS = centOS 7 64bit

6. Virtal Machine Name : hadoop01

   `location : C:\Users\a\Documents\Virtual Machines\hadoop01` 지정

7. disk size : 20 GB

   store single file

   memory : 2 GB

8. centOS 설치





> 가상머신 ip 변경

1. cmd -> ipconfig
2. vmware adator VMnet8 있나 확인
3. vmnetcfg를 `C:\Program Files (x86)\VMware\VMware Player` 경로에 복사 후 실행
4. VMnet8 ip 111.1 로 변경







> 가상 머신 복제 방법

1. `C:\Users\a\Documents\Virtual Machines` 경로에 hadoop1를 복제
2. VMware Workstation 에서 Open a Virtual Machine 클릭
3. 복제한 hadoop2.vmx 선택

4. Edit virtual machine settings - Options - Virtual machine name 에서 이름 수정

   (hadoop1를 복제 했기 때문에 name이 hadoop1로 설정됨)

5. 실행후 i copted it 

6. remin later 





> Hadoop Machine 클러스터링

1. 바탕화면 우클릭 후 터미널 열기

2. 4개의 가상머신 터미널에서 ifconfig (윈도우 환경은 ipconfig) -> inet 확인

3. `hostnamectl set-hostname hadoop01`로 hostname 변경

4. 처음엔 hostname이 localhost로 설정 되어있음

5. ssh 192.168.111.128 로 2번 가상머신 ip 접속 및 pass 입력후 

6. 3번과 같이 작업해서 hadoop02, hadoop03, hadoop04 작업

   `systemctl list-units --type=service` : 서비스 상태 확인

   ` systemctl stop firewalld` : 방화벽 해제

   `systemctl disable firewalld` : 방화벽 해제 고정

   `systemctl status firewalld` :  방화벽 상태 확인

7. `ssh 192.168.111.128 "systemctl disable firewalld"` : 2번 머신 방화벽 해제 , 3,4번도 똑같이 작업

8. 도메인 등록

   ssh통신을 하기 위해 hadoop01에서 나머지 머신을 접근

   ip로 접근하기 불편하므로 호스트명을 등록해서 작업

   /etc/hosts 파일 수정

   hosts 우클릭 텍스트 편집기로 실행 후

   192.168.111.129 hadoop01
   192.168.111.128 hadoop02
   192.168.111.130 hadoop03
   192.168.111.131 hadoop04 로 수정

   `ssh` : Secure shell

   텔넷과 비슷한 개념

   서버와 클라이언트간의 텍스트기반으로 통신, 암호화해서 통신하기 위한 프로토콜

   하둡도 내부에서 ssh포로토콜을 이용해서 통신

   ​	

   

   

   

> 프로그램 설치

* Java
  - JDK 설치
    - x64.rpm으로 설치
* Hadoop
* Hadoop 설정
* Hadoop 프로그래밍 
  * hdfs
  * mapreduce
  * 고급프로그래밍밍(customizing)
* Hadoop Eco System 설치 후 테스트
  * flume
  * sqoop
  * hive
  * pig
  * mahout
* R



> 리눅스 명령어

`ssh hadoop02` 로 접속확인 

` scp` : 원격지 복사 명령어

` scp /etc/hosts root@hadoop02:/etc/hosts` :  1번 머신에서 2번 머신으로 hosts파일 원격 복사

` ssh hadoop02 "/etc/init.d/network restart"` : 원격으로 network restart

` [root@hadoop01 ~]#` : 쉘 프롬포트

`~` : 홈 디렉토리 = 계정명

​        특정 계정으로 로그인 했을 때 자동으로 위치하는 디렉토리

​		모든 계정은 자신만의 홈디렉토리를 갖는다.

​		root계정 : /root

​		일반계정 : /home/계정명

`/home` : 사용자 계정의 홈디렉토리

`/boot` : 부팅에 필요한 각종 설정파일이 위치하는 곳

`/root` : root계정의 홈디렉토리

`/bin` : 리눅스에서 사용할 수 있는 shell명령어가 위치하는 곳

`/sbin` : 시스템관리를 위한 명령어가 위치

`/etc` : 시스템관리를 위한 설정파일이 위치하는 디렉토리

​			 사용자정보, 파일시스템정보, 네트워크정보

`/tmp` : 시스템이 작업 중 사용하는 임시 폴더

`/var` : tmp와 유사 보통 로그 파일이 위치

`/lib` : 공통 라이브러리파일이 저장되는 위치

`/dev` : 장치가 위치하는 디렉토리 - 리눅스는 모든 장치를 파일로 인식

`/usr` : 윈도우의 program files와 동일

`/passwd 사용자 계정명  ` : 사용자 계정 비밀번호 설정 

`/etc/passwd | grep test` : test에 대한 정보만 출력 (필터링)

`rm -rf test` : test 파일 삭제

`mkdir -p  mytest1/mytest2/mytest3` : mytest1 폴더 안에 mytest2 안에 mytest3 생성

`rpm -Uvh` : 이전 버전이 있으면 업그레이드 + 설치되는 과정을 보여주기 + 설치과정에 #을 추가

`rpm -Uvh jdkjdk-8u301-linux-x64.rpm`  : 

