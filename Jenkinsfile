pipeline {
    agent any
    
    stages {
        stage('Compile Code') {
            steps {
                script {
                    dir ('/Users/jaruizf/repos/ejemplo-maven'){
                        sh 'mvn clean compile -e'
                    }
                }
            }
        }
        stage('Test Code') {
            steps {
                script {
                    dir ('/Users/jaruizf/repos/ejemplo-maven'){
                        sh 'mvn clean test -e'
                    }
                }
            }
        }
        stage('Jar Code') {
            steps {
                script {
                    dir ('/Users/jaruizf/repos/ejemplo-maven'){
                        sh 'mvn clean package -e'
                    }
                }
            }
        }
        stage('Sonar') {
          steps {
            script {
              def scannerHome = tool 'sonar-scanner';
              withSonarQubeEnv('sonar-server') { 
                sh "${scannerHome}/bin/sonar-scanner -Dsonar.projectKey=ejemplo-maven -Dsonar.projectBaseDir=/Users/jaruizf/repos/ejemplo-maven -Dsonar.sources=src -Dsonar.java.binaries=build"
              }
            }
          }
        }
        stage('UploadNexus') {
            steps {
                script {
                    nexusPublisher nexusInstanceId: 'nexus-dev2', nexusRepositoryId: 'test-repo', packages: [[$class: 'MavenPackage', mavenAssetList: [[classifier: '', extension: '', filePath: '/Users/jaruizf/repos/ejemplo-maven/build/DevOpsUsach2020-0.0.1.jar']], mavenCoordinate: [artifactId: 'DevOpsUsach2020', groupId: 'com.devopsusach2020', packaging: 'jar', version: '0.0.1']]]
                }
            }
        }
    }
}
