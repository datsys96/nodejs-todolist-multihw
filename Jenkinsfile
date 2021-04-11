pipeline {
     agent { label 'jenkinslave' }
     stages {
          stage("clone code") {
               steps {
                    git 'https://github.com/datsys96/nodejs-todolist-multihw.git'
               }
          }
          stage('Login Gitlab') {
            steps {
                sh 'docker login registry.gitlab.com -u nodejs-multihw -p aExPMWg6XC6swap6gjpy'
            }
            }
          stage("build image") {
               steps {
                    sh 'docker build -t registry.gitlab.com/tuandat96/nodejs-todolist-multihw2 .'
               }
          }
        stage('Push Image to Gitlab') {
            steps {
                sh 'docker push registry.gitlab.com/tuandat96/nodejs-todolist-multihw'
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
            emailext body: 'failure ${DEFAULT_SUBJECT}', subject: '${DEFAULT_CONTENT}', to: '$datbeo12c@gmail.com'
        }
        changed {
            emailext body: 'change ${DEFAULT_SUBJECT}', subject: '${DEFAULT_CONTENT}', to: 'datbeo12c@gmail.com'
        }
    }
}
