pipeline {
    agent any
    triggers {
        pollSCM('H/2 * * * *')
    }
    stages {
        stage('Build') {
         steps {
             println 'aca va el build'
             sh "./build.sh"

         }
         post{
                     always{
                          junit 'build/test-results/test/*.xml'
                         println "ava se exportan los resultados de los test unitarios"
                     }
         }

        }
        stage('Deploy') {
          steps {
              sh "./deploy.sh"
              println 'aca va el deploy'
          }
        }
        stage('Verify') {
           steps {
               sh "./verify.sh"
               println 'aca va el verify'
           }
           post{
                       always{
                            junit 'build/test-results/test/*.xml'
                       }
                    }
        }

    }
    post {
        success {
            echo 'El job finalizó OK! :)'
        }
        failure {
            echo 'El job rompio! :('
        }
    }
}