node {
    def app

    stage('Clone repository') {
        checkout scm
    }

    stage('Update GIT') {
            script {
                catchError(buildResult: 'SUCCESS', stageResult: 'FAILURE') {
                    withCredentials([usernamePassword(credentialsId: 'github', passwordVariable: 'GIT_PASSWORD', usernameVariable: 'GIT_USERNAME')]) {
                        sh "git config user.email meir@cloudride.co.il"
                        sh "git config user.name meirjob"
                        sh "sed -i 's+777644549717.dkr.ecr.eu-west-1.amazonaws.com/simpleapp.*+777644549717.dkr.ecr.us-east-1.amazonaws.com/simpleapp:${IMAGE_TAG}+g' deployment.yaml"
                        sh "git add ."
                        sh "git commit -m 'update image tag: ${env.BUILD_NUMBER}'"
                        sh "git push https://${GIT_USERNAME}:${GIT_PASSWORD}@github.com/${GIT_USERNAME}/kubernetesconfig.git HEAD:main"
      }
    }
  }
}
}
