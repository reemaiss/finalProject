pipeline {
  environment {
    registry = "rema2030/api:latest"
    registryCredential = 'remadockerhub'
  }
     agent any 
     stages {
        stage('Lint HTML') {
      steps {
        sh 'tidy -q -e *.html'
      }
    } 
    stage('build docker image'){
steps{
  script{
    image = docker.build("rema2030/api:latest")
    docker.withRegistry('','remadockerhub'){
      dockerImage.push()
    }  
  }
}
    }
     }
}