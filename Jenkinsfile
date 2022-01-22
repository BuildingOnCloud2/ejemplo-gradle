pipeline {
  agent any

//  def mavenscript = load 'maven.groovy'
//  def gradlescript= load 'gradle.groovy'

  parameters {
    choice choices: ['gradle', 'maven'], description: 'Select Building Tool', name: 'buidlTool'
  }       

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
