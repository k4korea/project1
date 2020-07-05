
 $ git add .

 $ git commit -m update
 [master b87a651] update
 1 file changed, 1 insertion(+), 4 deletions(-)

 $ git push


git remote add origin https://github.com/k4korea/project1.git
git add .
git commit -m "first commit"
git push -u origin master


또 다른 방법은 로컬 저장소에서 모든 오래된 가지를 정리하는 것입니다. 이렇게 하면 리모컨에서 이미 제거된 모든 로컬 분기가 삭제됩니다.
git remote prune origin --dry-run




git java
https://jojoldu.tistory.com/139

    CI/CD with Jenkins and Docker java
    https://medium.com/@khandelwal12nidhi/ci-cd-with-jenkins-and-ansible-e9163d4a6e82

    spinring Building with Docker Using Jenkins Pipelines  
    https://www.liatrio.com/blog/building-with-docker-using-jenkins-pipelines

    git-lab java
    https://miiingo.tistory.com/171


git docker hub 연동


    jenkins ( github 연동 발급)
    -----


    jenkins-token ( github 연동 발급)
    a47b05acdc44aa8feb1444b8475e99ec0a54fa2f


    [터널링 github]
    https://jojoldu.tistory.com/139

    1 .기준
    https://www.howtodo.cloud/devops/docker/2019/05/16/devops-application.html

    2. docker를 이용한 CI 구축 연습하기 (젠킨스, 슬랙)
    https://jojoldu.tistory.com/139

    [참고]

    https://bcho.tistory.com/1237

    https://ict-nroo.tistory.com/35

    https://galid1.tistory.com/466

    https://teichae.tistory.com/entry/Jenkins-Pipeline%EC%9D%84-%EC%9D%B4%EC%9A%A9%ED%95%9C-Docker-Image-Push

    [jenkins doc]
    https://wiki.jenkins.io/display/JENKINS/Building+a+software+project

    BUILD_NUMBER "153"과 같은 현재 빌드 번호
    BUILD_ID     "2005-08-22_23-59-59"(YYYY-MM-DD_hh-mm-ss, 버전 1.597 이후 소멸)와 같은 현재 빌드 ID
    BUILD_URL    이 빌드의 결과를 찾을 수 있는 URL(예: http://buildserver/jenkins/job/MyJobName/666/)
    NODE_NAME    현재 빌드가 실행 중인 노드의 이름입니다. 마스터 노드의 '마스터'와 같습니다.


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

[slack]

    블로그 슬랙 받기
    https://jojoldu.tistory.com/139
    https://dnight.tistory.com/entry/Jenkins-Slack-%EC%95%8C%EB%A6%BC-%EC%97%B0%EB%8F%99
    https://phoby.github.io/slack-jenkins-notification/

    슬랙노티 사이트 
    https://hooks.slack.com/services/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


    삼메 slack
    sm-cloud.slack.com
    채널
    #test-deploy
    curl -X POST -H 'Content-type: application/json' --data '{"text":"Hello, World!"}' https://hooks.slack.com/services/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

    2번째
    팀 하위 도메인: sm-cloud
    통합 토큰 자격 증명 ID: 값으로 사용하여 비밀 텍스트 자격 증명 만들기
    li8Rq0U1DwEYGYnUpbYuiYef
    li8Rq0U1DwEYGYnUpbYuiYef
    참고사이트
    https://api.slack.com/apps/A016HN79J9K/incoming-webhooks?

    jenkin plugin
    https://plugins.jenkins.io/

    jenkins script
    https://code-maven.com/jenkins-pipeline-get-previous-build-status

pipeline {
    agent { label 'master' }
    stages {
        stage('first') {
            steps {
                script {
                    last_started = env.STAGE_NAME
                    echo "in first"
                    def a = 0
                    def b = 10 / a
                }
            }
        }
        stage('second') {
            steps {
                script {
                    last_started = env.STAGE_NAME
                    echo "in second"
                }
            }
        }
    }
    post {
        failure {
            echo "last_started: $last_started"
        }
    }
}
 