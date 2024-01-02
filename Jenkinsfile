pipeline {
    agent any

    parameters {
        string(name: 'BUILD_NUMBER', defaultValue: '', description: 'Build Number from CI')
    }

    stages {
        stage('Use Build Number') {
            steps {
                echo "Received Build Number: ${params.BUILD_NUMBER}"
            }
        }

	stage('Editing Image Version') {            
            steps {
                echo 'Editing'
                withCredentials([usernamePassword(credentialsId: 'github-cred', usernameVariable: 'USERNAME_CD', passwordVariable: 'PASSWORD_CD')]) {    
	            sh '''
                        mv manifest/deployment.yaml manifest/tmp.yaml
                        cat manifest/tmp.yaml | envsubst > manifest/deployment.yaml
                        rm -f manifest/tmp.yaml
			git config user.email elnabatshy27@gmail.com
                        git config user.name MahmoudG27
			git config url."https://${USERNAME_CD}:${PASSWORD_CD}@github.com/".insteadOf "https://github.com/"
			git add .
                        git commit -m "Done by Jenkins Job change manifest: ${env.BUILD_NUMBER}"
                        git push https://github.com/MahmoudG27/ArgoCD.git master
                    '''
                }
            }
        }
    }
}
