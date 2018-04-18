pipeline {
  agent any
  stages {
    stage('clean') {
      steps {
        echo 'limpiando codigo'
        sh 'core/mvn clean'
      }
    }
    stage('test unittario') {
      steps {
        echo 'lanzando test unitarios'
        sh 'core/mvn test'
      }
    }
    stage('Empaquetado') {
      parallel {
        stage('Empaquetado') {
          steps {
            echo 'Generacion de war'
            sh 'core/mvn package'
          }
        }
        stage('Lanzo Sonar') {
          steps {
            echo 'LAnzando sonar'
            sh 'cd core mvn sonar:sonar'
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
        sh 'cd core mvn install'
      }
    }
  }
}
