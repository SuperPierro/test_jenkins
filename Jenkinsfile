pipeline {
    agent any

    environment {
        VERSION_NUMBER = '6.2.3'
        PASSWORD = 'abc123'
    }

    stages {
        stage('Initialisation'){
            steps {
                echo "JeskinsFile version : ${VERSION_NUMBER}\n"
                echo "Please use following credentials to connect:\n"
                echo "\t id : admin\n\t pwd : ${PASSWORD}"
            }
        }

        stage('Sanity check') {
            steps {
                // input "Does the staging environment look ok?"
                echo 'ca marche pas'
            }
        }

        stage('Rectification'){
            environment {
                TRUE_CRED = credentials('TEST_CRED')
            }
            steps {
                echo "Nan les vraies infos sont stockées dirrectement dans Jeskins\n"
                echo "Please use following credentials to connect:\n"
                echo "\t id : admin\n\t pwd : ${TRUE_CRED_PSW}"
            }
        }

        stage('Build') {
            steps {
                sh 'echo "CA a l air de marcher mouahahaha"'
                sh '''
                    echo "Multiline shell steps works too"
                    ls -lah
                '''
            }
        }

		stage('Deploy') {
		    steps {
				retry(3) {
			   		sh './bonjour.sh'
				}

				timeout(time: 3,unit: 'MINUTES'){
			    	sh './health-check.sh'
				}

		    }
		}

        /*
        stage ('Report') { 
          steps {
            // install required gems
            sh 'bundle install'

            // build and run tests with coverage
            sh 'bundle exec rake build spec'

            // Archive the built artifacts
            archive includes: 'pkg/*.gem'

            // publish html
            publishHTML target: [
                allowMissing: false,
                alwaysLinkToLastBuild: false,
                keepAll: true,
                reportDir: 'coverage',
                reportFiles: 'index.html',
                reportName: 'RCov Report'
              ]
          }
        }*/
    }

    post {
    	always {
    		echo 'this will always run'
            /* mail to: 'poirier.pier@gmail.com',
             * subject: "Failed Pipeline: ${currentBuild.fullDisplayName}",
             * body: "Something is wrong with ${env.BUILD_URL}"
             */
    	}

    	success {
    		echo 'he bah mon vieux chai pas comment t\'as fais ca mais ca marche'
    	}

    	failure {
    		echo 't\'as tout cassé...'
    	}
    }
}
