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
  post {
    always {
      println 'Checking Pipeline Status'
    }
    failure {
      slackSend color: '#BADA55', message: 'Jesus Ruiz ${env.JOB_NAME}' + params.buildTool + 'Ejecucion exitosa'
    }
    success {
      slackSend color: '#BADA55', message: 'Jesus Ruiz ${env.JOB_NAME}' + params.buildTool + 'Ejecucion fallida en stage ${env.STAGE_NAME}'
    }
  }
}
