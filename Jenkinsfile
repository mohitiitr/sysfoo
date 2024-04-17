pipeline {
  agent any
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
  tools {
    maven '3.6.3'
  }
  post {
    always {
      echo 'This pipeline is completed..'
    }

  }
}
