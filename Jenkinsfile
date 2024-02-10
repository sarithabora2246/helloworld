pipeline {
  agent any
  tools { 
      maven 'maven3' 
  }
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
   /*stage("Scan") {
          steps {
              withSonarQubeEnv(installationName: 'sonarqube_token') {
                 sh 'mvn clean org.sonarsource.scanner.maven:sonar-maven-plugin:3.9.0.2155:sonar'
              }
          }
      }*/
    stage("Deploy") {
          steps {
              script {
                // deploy adapters: [tomcat9(credentialsId: 'tomcat_deployer', path: '', url: 'http://18.218.56.147:8080/')], contextPath: '/app', onFailure: false, war: 'webapps/target/*.war' 
                    deploy adapters: [tomcat9(url: 'http://3.138.119.67:8080/',
                      credentialsId: 'tomcat_deployer')],
                      war: 'webapp/target/*.war',
                      contextPath: '/examples'
              }
          }
      }


    
}
}
