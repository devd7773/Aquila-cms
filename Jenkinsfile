pipeline {
        agent {
              label "Aquila-cms"
        }
        stages {
             stage("pulling the code from scm") {
                  steps {
                        git branch: 'main', url: 'https://github.com/devd7773/Aquila-cms.git'
                  }
             }
             stage("build the image from dockerfile") {
                  steps {
                        sh "docker build -t aquila:$BUILD_TAG ."
                        sh "docker tag aquila:$BUILD_TAG dev7773/aquila:$BUILD_TAG"
                  }
             }
             stage("push the docker") {
                  steps {
                        withCredentials([string(credentialsId: 'docker-hub-cred', variable: 'my_cred')]) {
                                sh "docker login -u dev7773 -p ${my_cred}"
                                sh "docker push dev7773/aquila:$BUILD_TAG"
                        }
                  }
             }
             stage("test the code in docker container") {
                  steps {
                        sh "docker run -dit --name aquila-cms -p 80:3010 dev7773/aquila:latest"
                  }
             }

        }

}



