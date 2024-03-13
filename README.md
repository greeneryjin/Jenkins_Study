# Jenkins_Study

## 개발 목적 ##

-> aws ubuntu의 빌드한 jar파일을 젠킨스로 AWS ubuntu에 옮기기 (개발 서버에서 완료된 코드를 운영 서버에서 젠킨스로 배포)


### 서버 구성 ###

<img width="357" alt="젠킨스 서버 구성도" src="https://github.com/greeneryjin/Jenkins_Study/assets/87289562/9596d4ca-4946-4c22-9704-63a274247020">

1. docker에 Jenkins 설치

       docker run --privileged -d -p 8080:8080 --name jenkins jenkins/jenkins

       # 비밀번호 확인
       docker exec jenkins sh -c 'cat /var/jenkins_home/secrets/initialAdminPassword'

2. 젠킨스 SSH 연결

        1. 젠킨스에 publish over ssh 설치
        2. 젠킨스 관리 → 플러그인 → publish over ssh 설정 탭
        3. SSH 설정
        4. key에 aws ubuntu pem key 값 넣기 
        a. ssh server:이름 작성
        b. Hostname: aws ip 
        c. Remote Directory: /home/ubuntu
        

3. 젠킨스 파이프 라인 

        1. GitHub project 선택
        2. GitHub hook tigger for GITScm polling 선택
        3. 파이프라인
        pipeline syntax 클릭

        pipeline syntax 페이지 
        steps에서 sshPublisher: Send build artifacts over SSH 클릭
    
        SSH Publishers 탭
        Transfers 
        Source files: build/libs/*SNAPSHOT.jar
        Remove prefix: build/libs
        Remote directory: /폴더이름(test1)
        Exec commend: 적당한 shell 명령어 넣기
        Gnearate Pipeline Script 클릭


   
