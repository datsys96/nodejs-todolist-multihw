pipeline {
     agent { label 'jenkinslave' }
     environment {
        scannerHome = tool 'sonarscan'
     }
     stages {
          stage("clone code") {
               steps {
                    git 'https://github.com/datsys96/nodejs-todolist-multihw.git'
               }
          }
           stage("sona scaner") {
               steps {
               withSonarQubeEnv('sonarscan') {
                sh "${scannerHome}/bin/sonar-scanner"
               }
                waitForQualityGate abortPipeline: true
          }
                }
          stage("test junit") {
               steps {
		junit 'testmulti.xml'
               }
          }
     }

    post {
        always {
	emailext body: 'helle day la jenkin nha', subject: 'test jenkin', to: 'datbeo12c@gmail.com'
        }
	        success {
            emailext body: 'ok ${DEFAULT_SUBJECT}', subject: '${DEFAULT_CONTENT}', to: 'datbeo12c@gmail.com'
        }
        unstable {
            emailext body: 'unstable ${DEFAULT_SUBJECT}', subject: '${DEFAULT_CONTENT}', to: 'datbeo12c@gmail.com'
        }
        failure {
            emailext body: 'failure ${DEFAULT_SUBJECT}', subject: '${DEFAULT_CONTENT}', to: 'datbeo12c@gmail.com'
        }
        changed {
            emailext body: 'change ${DEFAULT_SUBJECT}', subject: '${DEFAULT_CONTENT}', to: 'datbeo12c@gmail.com'
        }
    }
}
