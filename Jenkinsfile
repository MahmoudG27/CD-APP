node {
    def manifest

    stage('Clone repository') {
        checkout scm
    }
    parameters {
        string(name: 'FROM_BUILD', defaultValue: '', description: 'Build Number CI Pipeline')
    }

    stage('Update GIT') {
        script {
            catchError(buildResult: 'SUCCESS', stageResult: 'FAILURE') {
                withCredentials([usernamePassword(credentialsId: 'github-cred', passwordVariable: 'GIT_PASSWORD', usernameVariable: 'GIT_USERNAME')]) {
                        sh "git config user.email elnabatshy27@gmail.com"
                        sh "git config user.name MahmoudG27"
                        sh "sh artifact_version manifest/deployment.yaml"
                        sh "echo $FROM_BUILD"
                        sh "git add ."
                        sh "git commit -m 'Done by Jenkins Job change manifest: ${env.FROM_BUILD}'"
                        sh "git push https://${GIT_USERNAME}:${GIT_PASSWORD}@github.com/${GIT_USERNAME}/CD-APP/ master"
      		}
    	    }
  	}
    }
}
