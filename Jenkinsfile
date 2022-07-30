pipeline {
  environment {
    imagename = "josesegurapersistent/flaskapp"
    registryCredential = 'josesegurapersistent'
    dockerImage = ''
  }
  agent any
  stages {
    stage('Cloning Git') {
      steps {
        git([url: 'https://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@github.com/josesegura-persistent/ResultadosEnVivo.git', branch: 'master'])
 
      }
    }
    stage('Building image') {
      steps{
        script {
          dockerImage = docker.build imagename
        }
      }
    }
    stage('Deploy Image') {
      steps{
        script {
          docker.withRegistry( '', registryCredential ) {
            dockerImage.push("$BUILD_NUMBER")
             dockerImage.push('latest')
          }
        }
      }
    }
    stage('Remove Unused docker image') {
      steps{
        sh "docker rmi $imagename:$BUILD_NUMBER"
         sh "docker rmi $imagename:latest"
 
      }
    }
  }
}
