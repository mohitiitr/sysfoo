pipeline {
  agent {
    docker {
      image 'maven:3.6.3-jdk-11-slim'
    }

  }
  stages {
    stage('build') {
      steps {
        echo 'compiling the code'
        sh 'mvn compile'
      }
    }

    stage('test') {
      steps {
        echo 'executing the tests'
        sh 'mvn clean test'
      }
    }

    stage('package') {
      when {
        branch 'master'
      }
      steps {
        echo 'packaging the build'
        sh 'mvn package -DskipTests'
      }
    }

    stage('archival') {
      when {
        branch 'master'
      }
      steps {
        archiveArtifacts 'target/*.war'
        echo 'Artifacts Archived'
      }
    }

  }
  post {
    always {
      echo 'This pipeline is completed..'
    }

  }
}
