def imageName = 'sonatypenexus/helloworld'
def registry  = 'http://20.163.196.201:9091/repository/docker/'
def version   = '1.0.2'
pipeline {
  agent any
  stages {
    stage('Checkout') {
      steps {
        git branch: 'main', url: 'https://github.com/bkrraj/helloworld.git'
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
        sh '/opt/apache-maven/bin/mvn clean install'
        echo '<------------- Build completed --------------->'
      }
    }
    stage('Unit Test') {
      steps {
        echo '<--------------- Unit Testing started  --------------->'
        sh '/opt/apache-maven/bin/mvn surefire-report:report'
        echo '<------------- Unit Testing stopped  --------------->'
      }
    }
    
}
}
