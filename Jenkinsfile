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
             withSonarQubeEnv('sonar') {
             //     echo ${scannerHome}
              
        sh "/home/vagrant/.jenkins/tools/hudson.plugins.sonar.SonarRunnerInstallation/sonar_scanenr_3.1.0/bin/sonar-scanner -Dsonar.projectName=curso_j-nkins -Dsonar.projectVersion=1 -Dsonar.projectKey=curso-jenkins -Dsonar.sources=. -Dsonar.java.binaries=core/target/classes"
       }

          }
        }
      }
    }
    stage('sonar Quality gate') {
      steps {
         timeout(time: 10, unit: 'MINUTES') {
           def qg = waitForQualityGate() // Reuse taskId previously collected by withSonarQubeEnv
    if (qg.status != 'OK') {
      error "Pipeline aborted due to quality gate failure: ${qg.status}"
         //   waitForQualityGate abortPipeline: true
              }
          }  
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
