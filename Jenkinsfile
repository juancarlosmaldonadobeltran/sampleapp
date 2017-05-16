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
        bat 'mvn clean test'
        junit 'target/surefire-reports/*.xml'
        bat 'mvn verify -DskipUTs'
      }
    }
    stage('Resultados Test') {
      steps {
        junit 'target/failsafe-reports/*.xml'
      }
    }
    stage('Analisis de codigo') {
      steps {
        bat 'mvn -DskipTest checkstyle:checkstyle pmd:pmd findbugs:findbugs'
        checkstyle(pattern: 'target/checkstyle-result.xml')
        findbugs(pattern: 'target/findbugs.xml')
        pmd(pattern: 'target/pmd.xml')
      }
    }
    stage('Generar artefacto') {
      steps {
        bat 'mvn clean package -DskipTests'
        archiveArtifacts 'target/webapp*.jar'
      }
    }
  }
}