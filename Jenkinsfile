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
   stage('Docker Build') {
      agent any
      steps {
        sh 'docker build -t josesegurapersistent/flaskapp:latest .'
      }
   }
    stage('Docker Push') {
      agent any
      steps {
        withCredentials([usernamePassword(credentialsId: 'dockercredentials', passwordVariable: 'dockerHubPassword', usernameVariable: 'dockerHubUser')]) {
          sh "docker login -u ${env.dockerHubUser} -p ${env.dockerHubPassword}"
          sh 'docker push shanem/spring-petclinic:latest'
        }
      }
    }
  }
}
