pipeline {
  agent {
    docker {
      image 'maven:3.3.9-jdk-8'
      args '-p 3000:3000'
    }

  }
  stages {
    stage('Initialize') {
      steps {
        sh '''echo PATH = ${PATH}
echo M2_HOME = ${M2_HOME}
mvn clean'''
      }
    }
    stage('Build') {
      steps {
        sh 'mvn -Dmaven.test.failure.ignore=true install'
      }
    }
    stage('Report') {
      steps {
        junit '/sys/firmware/reports'
        archiveArtifacts '/sys/firmware/archive'
      }
    }
  }
}