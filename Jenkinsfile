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
          sh 'nohup gradle bootRun &'
          sleep 15
        }
      }
    }
    stage('test') {
      steps {
        script {
          println "Stage: ${env.STAGE_NAME}"
          sh 'gradle clean test'
        }
      }
    }
    stage('nexus') {
      steps {
        script {
          println "Stage: ${env.STAGE_NAME}"
          nexusPublisher nexusInstanceId: 'nexus-local', nexusRepositoryId: 'test-nexus', packages: [[$class: 'MavenPackage', mavenAssetList: [[classifier: '', extension: '', filePath: '/Users/jaruizf/repos/ejemplo-gradle/build/libs/DevOpsUsach2020-0.0.1.jar']], mavenCoordinate: [artifactId: 'DevOpsUsach2020', groupId: 'com.devopsusach2020', packaging: 'jar', version: '0.0.1']]]
        }
      }
    }
  }
}
