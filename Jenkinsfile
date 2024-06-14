pipeline {
    agent any
    stages {
        stage('Build') { 
            steps {
                sh 'npm install' 
            }
        }
		stage('Test') {
			steps {
				sh './jenkins/scripts/test.sh'
			}
		}
		stage('Deliver') {
			steps {
				sh './jenkins/scripts/deliver.sh'
				input message: 'Finished using the website? (Click "Proceed" to continue)'
				sh './jenkins/scripts/kill.sh'
			}
		}
    }
	post {
		stage('Notify Discord') {
			steps {
				discordSend {
					webhookURL: 'https://discord.com/api/webhooks/1251172647086194828/YGgeMJ_e1mFw7jmt-UC67A17H9dw1oXyrVqKyBsqhmm3o3_ytox_1GaXNqfpa6DmHv8V',
					description: 'hi from *Jenkins*'
				}
			}
		}
	}
}
