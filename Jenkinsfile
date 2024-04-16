pipeline {
  agent any
  tools {
    maven '3.6.3'
  }
  stages{
      stage("build"){
          steps{
              echo 'compiling the code'
              sh 'mvn compile'
          }
      }
      stage("test"){
          steps{
              echo 'executing the tests'
              sh 'mvn clean test'
          }
      }
      stage("package"){
          steps{
              echo 'packaging the build'
              sh 'mvn package -DskipTests'
          }
      }
  }

  post{
    always{
        echo 'This pipeline is completed..'
    }
  }
}
