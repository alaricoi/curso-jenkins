pipeline {
  agent any
  stages {
    stage('clean') {
      steps {
        echo 'limpiando codigo'
        sh 'mvn clean'
      }
    }
    stage('test unittario') {
      steps {
        echo 'lanzando test unitarios'
        sh 'mvn test'
      }
    }
    stage('Empaquetado') {
      parallel {
        stage('Empaquetado') {
          steps {
            echo 'Generacion de war'
            sh 'mvn package'
          }
        }
        stage('Lanzo Sonar') {
          steps {
            echo 'LAnzando sonar'
            sh 'mvn sonar:sonar'
          }
        }
      }
    }
    stage('sonar Quality gate') {
      steps {
        waitForQualityGate true
      }
    }
    stage('') {
      steps {
        echo 'Instalar'
        sh 'mvn install'
      }
    }
  }
}