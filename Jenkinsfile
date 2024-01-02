pipeline {
    agent any

    parameters {
        string(name: 'FROM_BUILD', defaultValue: '', description: 'Build Number CI Pipeline')
    }

    stages {
	 
	stage('Use Build Number') {
            steps {
                echo "Received Build Number: ${params.FROM_BUILD}"
            }
        }

	stage('Editing Image Version') {            
            steps {
                echo 'Editing'
                withCredentials([usernamePassword(credentialsId: 'github-cred', usernameVariable: 'USERNAME_CD', passwordVariable: 'PASSWORD_CD')]) {    
	            sh '''
			sh artifact_version
			git config user.email elnabatshy27@gmail.com
                        git config user.name MahmoudG27
			git add . 
                        git commit -m "Done by Jenkins Job changemanifest: ${params.FROM_BUILD}"
                        git push https://${USERNAME_CD}:${PASSWORD_CD}@github.com/${USERNAME_CD}/CD-APP/ HEAD:master"
                    '''
                }
            }
        }
    }
}
