pipeline {
  agent any
  stages {
    stage('Checkout') {
      steps {
        git branch: 'main', url: 'https://github.com/sarithabora2246/helloworld.git'
      }
    }
    stage('Pull Changes') {
      steps {
        sh 'git pull origin main'
      }
    }
    stage('Build') {
      steps {
        echo '<--------------- Building --------------->'
        sh 'printenv'
        sh 'mvn clean install'
        echo '<------------- Build completed --------------->'
      }
    }
    stage('Unit Test') {
      steps {
        echo '<--------------- Unit Testing started  --------------->'
        sh 'mvn surefire-report:report'
        echo '<------------- Unit Testing stopped  --------------->'
      }
    }
    stage('Sonar Analysis') {
      environment {
        scannerHome = tool 'sonarqube'
      }
      steps {
        echo '<--------------- Sonar Analysis started  --------------->'
                // withSonarQubeEnv('SonarServer') {
                //     sh "${scannerHome}/bin/sonar-scanner"

        // }
        withSonarQubeEnv('sonarqube_token') {
          sh 'mvn clean package sonar:sonar'
          echo '<--------------- Sonar Analysis stopped  --------------->'
        }
      }
    }
    stage('Quality Gate') {
      steps {
        script {
          echo '<--------------- Quality Gate started  --------------->'
          timeout(time: 1, unit: 'MINUTES') {
            def qg = waitForQualityGate()
            if (qg.status != 'OK') {
              error 'Pipeline failed due to the Quality gate issue'
            }
          }
          echo '<--------------- Quality Gate stopped  --------------->'
        }
      }
    }
    
}
}
