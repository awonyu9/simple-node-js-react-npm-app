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
				// input message: 'Finished using the website? (Click "Proceed" to continue)'
				sh './jenkins/scripts/kill.sh'
			}
		}
    }
	post {
		success {
			discordSend(
				webhookURL: "https://discord.com/api/webhooks/1251172647086194828/YGgeMJ_e1mFw7jmt-UC67A17H9dw1oXyrVqKyBsqhmm3o3_ytox_1GaXNqfpa6DmHv8V",
				title: 'simple-node-app - Jenkins build success',
				link: env.BUILD_URL,
				result: SUCCESS,
			)
		}
		unsuccessful {
			discordSend(
				webhookURL: "https://discord.com/api/webhooks/1251172647086194828/YGgeMJ_e1mFw7jmt-UC67A17H9dw1oXyrVqKyBsqhmm3o3_ytox_1GaXNqfpa6DmHv8V",
				title: "simple-node-app - Jenkins build failure",
				link: env.BUILD_URL,
				result: FAILURE
			)
		}
	}
}
