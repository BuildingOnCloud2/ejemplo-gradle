pipeline {
  agent any
    
  stages {
    stage('Build & Unit Test') {
      steps {
        script {
          println "Stage: ${env.STAGE_NAME}"
          sh 'gradle clean build'
        }
      }
    }
    stage('sonar') {
      steps {
        script {
          println "Stage: ${env.STAGE_NAME}"
          def scannerHome = tool 'sonar-scanner';
          withSonarQubeEnv('sonar-server') { 
            sh "${scannerHome}/bin/sonar-scanner -Dsonar.projectKey=ejemplo-gradle -Dsonar.projectBaseDir=/Users/jaruizf/repos/ejemplo-gradle -Dsonar.sources=src -Dsonar.java.binaries=build"
          }
        }
      }
    }
    stage('run') {
      steps {
        script {
          println "Stage: ${env.STAGE_NAME}"
          sh 'nohup bash gradle bootRun &'
          sleep 15
        }
      }
    }
    stage('test') {
      steps {
        script {
          println "Stage: ${env.STAGE_NAME}"
        }
      }
    }
    stage('nexus') {
      steps {
        script {
          println "Stage: ${env.STAGE_NAME}"
        }
      }
    }
  }
}
