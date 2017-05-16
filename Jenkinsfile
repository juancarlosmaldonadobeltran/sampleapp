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
            git 'https://github.com/juancarlosmaldonadobeltran/sampleapp.git'
            
          }
        )
      }
    }
    stage('Test Maven') {
      steps {
        sh 'mvn clean test'
      }
    }
  }
}