node {
    def manifest

    stage('Clone repository') {
        checkout scm
    }

    stage('Update GIT') {
        script {
            catchError(buildResult: 'SUCCESS', stageResult: 'FAILURE') {
                withCredentials([usernamePassword(credentialsId: 'github-cred', passwordVariable: 'GIT_PASSWORD', usernameVariable: 'GIT_USERNAME')]) {
			sh "git config user.email elnabatshy27@gmail.com"
                        sh "git config user.name MahmoudG27"
			sh "git config url.'https://${GIT_USERNAME}:${GIT_PASSWORD}@github.com/'.insteadOf 'https://github.com/'"
			sh "cat manifest/deployment.yaml"
			sh "sh artifact_version manifest/deployment.yaml"
                        sh "echo $FROM_BUILD"
                        sh "cat manifest/deployment.yaml"
			sh "git add ."
                        sh "git commit -m 'Done by Jenkins Job change manifest:${env.FROM_BUILD}'"
                        sh "git push https://github.com/MahmoudG27/CD-APP.git master"
      		}
    	    }
  	}
    }
}
