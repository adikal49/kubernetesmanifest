node {
    def app

    stage('Clone repository') {
      

        checkout scm
    }

    stage('Update GIT') {
            script {
                catchError(buildResult: 'SUCCESS', stageResult: 'FAILURE') {
                    withCredentials([usernamePassword(credentialsId: 'github', passwordVariable: 'GIT_PASSWORD', usernameVariable: 'GIT_USERNAME')]) {
                        //def encodedPassword = URLEncoder.encode("$GIT_PASSWORD",'UTF-8')
                        //env.DOCKERHUB_USERNAME = "adicop"
                        //env.APP_NAME = "test"
                        //env.IMAGE_NAME = "${env.DOCKERHUB_USERNAME}" + "/" + "${env.APP_NAME}"
                        sh "git config user.email adicop49@gmail.com"
                        sh "git config user.name adikal49"
                        //sh "git switch master"
                        sh "cat deployment.yaml"
                        //sh "sed -i 's/${APP_NAME}.*/${APP_NAME}:${IMAGE_TAG}/g' deployment.yml"
                        sh "sed -i 's+adicop/test.*+adicop49/test:${DOCKERTAG}+g' deployment.yaml"
                        //sh "sed -i 's/${IMAGE_NAME}.*/${IMAGE_NAME}:${DOCKERTAG}/g' deployment.yaml"
                        sh "cat deployment.yaml"
                        sh "git add ."
                        sh "git commit -m 'Done by Jenkins Job changemanifest: ${env.BUILD_NUMBER}'"
                        sh "git push https://${GIT_USERNAME}:${GIT_PASSWORD}@github.com/${GIT_USERNAME}/kubernetesmanifest.git main"
      }
    }
  }
}
}
