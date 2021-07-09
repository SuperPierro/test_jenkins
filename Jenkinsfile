pipeline {
    agent any
    stages {
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
    }

    post {
    	always {
    		echo 'this will always run'
    	}

    	success {
    		echo 'he bah mon vieux chai pas comment t\'as fais ca mais ca marche'
    	}

    	failure {
    		echo 't\'as tout cassé...'
    	}
    }
}
