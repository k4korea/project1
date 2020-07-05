
git java
https://jojoldu.tistory.com/139

    CI/CD with Jenkins and Docker java
    https://medium.com/@khandelwal12nidhi/ci-cd-with-jenkins-and-ansible-e9163d4a6e82

    spinring Building with Docker Using Jenkins Pipelines  
    https://www.liatrio.com/blog/building-with-docker-using-jenkins-pipelines

    git-lab java
    https://miiingo.tistory.com/171


git docker hub 연동
[터널링 github]
https://jojoldu.tistory.com/139

[기준]
https://www.howtodo.cloud/devops/docker/2019/05/16/devops-application.html

    2. docker를 이용한 CI 구축 연습하기 (젠킨스, 슬랙)
    https://jojoldu.tistory.com/139

[참고]

https://bcho.tistory.com/1237

https://ict-nroo.tistory.com/35

https://galid1.tistory.com/466

https://teichae.tistory.com/entry/Jenkins-Pipeline%EC%9D%84-%EC%9D%B4%EC%9A%A9%ED%95%9C-Docker-Image-Push


[jenkins docker run]
http://blog.naver.com/PostView.nhn?blogId=rudnfskf2&logNo=221466146654&parentCategoryNo=&categoryNo=58&viewDate=&isShowPopularPosts=true&from=search
docker run -d \   # 데몬으로 젠킨스를 실행
-p 8080:8080 \    # 도커 컨테이너의 포트를 HOST인 AWS서버의 포트와 연결해주는 포워딩
-p 9999:9999 \    # 나중에 실습할 Slave PC와 연결하기위한 포트 포워딩
-v ~/docker/jenkins:/var/jenkins_home # Host의 ~/docker/jenkins폴더에 컨테이너의 /var/jenkins_home을 마운트하기
-u root \ # 컨테이너를 루트 권한으로 실행
jenkins # 젠킨스 이미지로 부터 컨테이너 생성
[출처] 1. Jenkins Declarative pipeline 튜토리얼(Docker Image로 Jenkins 설치 + Github연동 + Pipeline으로 Helloworld 출력)|작성자 David

docker run -d -p 8080:8080 -p 9999:9999 -v ~/docker/jenkins:/var/jenkins_home -u root jenkins



[멋진놈]
https://yookeun.github.io/




jenkinsfile


#변경점
     stage('Build image') {
         app = docker.build("teichae/jenkins") #Push Image 단계에서 빌드번호를 붙이기 때문에 옵션 제거
     }
     stage('Push image') {
         docker.withRegistry('https://registry.hub.docker.com', 'docker-hub') #업로드할 레지스트리 정보, Jenkins Credentials ID {
             app.push("${env.BUILD_NUMBER}") #image에 빌드번호를 태그로 붙인 후 Push
             app.push("latest") #image에 latest를 태그로 붙인 후 Push
     }
  }
}