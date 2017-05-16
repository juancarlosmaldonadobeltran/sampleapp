pipeline {
  agent any
  stages {
    stage('Saludo') {
      steps {
        parallel(
          "Saludo": {
            echo 'Hello world DevOps!'
            
          },
          "Obtener cambios SCM": {
            git 'git@github.com:juancarlosmaldonadobeltran/sampleapp.git'
            
          }
        )
      }
    }
    stage('Test Maven') {
      steps {
        bat 'mvn clean test'
      }
    }
  }
}