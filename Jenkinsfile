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
                        sh "docker build -t my-app:$BUILD_TAG ."
                  }
             }
             stage("test the code in docker container") {
                  steps {
                        sh "docker run -dit --name aquila-cms -p 80:3010 my-app:$BUILD_TAG"
                  }
             }

        }

}



