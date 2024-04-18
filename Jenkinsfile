pipeline {
  agent none
  stages {
    stage('build') {
      agent {
        docker {
          image 'maven:3.6.3-jdk-11-slim'
        }

      }
      steps {
        echo 'compiling the code'
        sh 'mvn compile'
      }
    }

    stage('test') {
      agent {
        docker {
          image 'maven:3.6.3-jdk-11-slim'
        }

      }
      steps {
        echo 'executing the tests'
        sh 'mvn clean test'
      }
    }

    stage('package') {
      parallel {
        stage('package') {
          agent {
            docker {
              image 'maven:3.6.3-jdk-11-slim'
            }

          }
          when {
            branch 'master'
          }
          steps {
            echo 'packaging the build'
            sh 'mvn package -DskipTests'
            echo 'archiving artifacts'
            archiveArtifacts 'target/*.war'
          }
        }

        stage('Docker BnP') {
          steps {
            script {
              docker.withRegistry('https://index.docker.io/v1/', 'dockerlogin') {
                def dockerImage = docker.build("mkumar2iitr/sysfoo:v${env.BUILD_ID}", "./")
                dockerImage.push()
                dockerImage.push("latest")
                dockerImage.push("dev")
              }
            }

          }
        }

      }
    }

  }
  post {
    always {
      echo 'This pipeline is completed..'
    }

  }
}