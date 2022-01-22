pipeline {
  agent any


  parameters {
    choice choices: ['gradle', 'maven'], description: 'Select Building Tool', name: 'buildTool'
  }       

stages{
    stage('Pipeline'){
      steps{
        script{
          println "Stage: ${env.STAGE_NAME}"
          if (params.buildTool=="gradle") {
              println "Executing Gradle"
              def gradlescript = load 'gradle.groovy'
              gradlescript.call()
          } else {
              println "Executing Maven"
              def mavenscript  = load 'maven.groovy'
              mavenscript.call()
          }
        }
      }
    }
  }
}
