pipeline {
  agent {
    docker {
      image 'maven:3.5-alpine'
    }
    
  }
  stages {
    stage('SCM') {
      steps {
        git(url: 'https://github.com/adrianmoya/sampleapp', branch: 'master')
      }
    }
    stage('Unit tests') {
      steps {
        sh 'mvn test'
      }
    }
    stage('Report UTs') {
      steps {
        junit 'target/surefire-reports/*.xml'
      }
    }
    stage('Integration Tests') {
      steps {
        sh 'mvn clean verify -DskipUTs'
      }
    }
    stage('Report ITs') {
      steps {
        junit 'target/failsafe-reports/*.xml'
      }
    }
  }
}