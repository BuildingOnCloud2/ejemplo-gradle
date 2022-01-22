pipeline {
  agent any

//  def mavenscript = load 'maven.groovy'
//  def gradlescript= load 'gradle.groovy'

  stages{
    stage('Pipeline'){
      steps{
        script{
              println "Stage: ${env.STAGE_NAME}"
        }
      }
    }
  }
}
