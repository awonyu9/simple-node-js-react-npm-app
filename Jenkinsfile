pipeline {
    agent any
	environment {
		// DISCORD_WEBHOOK_URL = "https://discord.com/api/webhooks/1251172647086194828/YGgeMJ_e1mFw7jmt-UC67A17H9dw1oXyrVqKyBsqhmm3o3_ytox_1GaXNqfpa6DmHv8V"
		DISCORD_WEBHOOK_URL = "https://discord.com/api/webhooks/1256231536332902492/p0Q79BwJUTDIxpNuDDzE9cRDbF_s-LWvnX5TWYbrfGKOVZH76eR3bQoF_kcjShLmb2Yr"
	}
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
		success {
			discordSend(
				webhookURL: DISCORD_WEBHOOK_URL,
				title: "${env.JOB_NAME} - Jenkins build success",
				link: env.BUILD_URL,
				result: "SUCCESS",
			)
		}
		unsuccessful {
			discordSend(
				webhookURL: DISCORD_WEBHOOK_URL,
				title: "${env.JOB_NAME} - Jenkins build failure",
				link: env.BUILD_URL,
				result: "FAILURE"
			)
		}
	}
}
