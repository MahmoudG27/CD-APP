pipeline {
    agent any

    stages {

	stage('Editing Image Version') {            
            steps {
                echo 'Editing'
                withCredentials([usernamePassword(credentialsId: 'github-cred', usernameVariable: 'USERNAME_CD', passwordVariable: 'PASSWORD_CD')]) {    
	            sh '''
                        mv manifasts/deployment.yaml manifasts/tmp.yaml
                        cat manifasts/tmp.yaml | envsubst > manifasts/deployment.yaml
                        rm -f manifasts/tmp.yaml
			git config user.email elnabatshy27@gmail.com
                        git config user.name MahmoudG27
			git add .
                        git commit -m 'Done by Jenkins Job changemanifest: ${env.BUILD_NUMBER}'
                        git push https://${USERNAME_CD}:${PASSWORD_CD}@github.com/${USERNAME_CD}/CD-APP/ HEAD:master"
                    '''
                }
            }
        }
    }
}
