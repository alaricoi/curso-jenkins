pipeline {
  agent any
  stages {
    stage('clean') {
      steps {
        echo 'limpiando codigo'
        sh 'cd core mvn clean'
      }
    }
    stage('test unittario') {
      steps {
        echo 'lanzando test unitarios'
        sh 'cd core mvn test'
      }
    }
    stage('Empaquetado') {
      parallel {
        stage('Empaquetado') {
          steps {
            echo 'Generacion de war'
            sh 'cd core vn package'
          }
        }
        stage('Lanzo Sonar') {
          steps {
            echo 'LAnzando sonar'
            //sh 'cd core mvn sonar:sonar'
             withSonarQubeEnv('sonar scanner 3.1.0') {
                sh "${scannerHome}/bin/sonar-scanner"
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
