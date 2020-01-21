pipeline {
  environment {
    registry = "rema2030/api:latest"
    registryCredential = 'dockerhub'
  }
     agent any 
     stages {
        stage('Lint HTML') {
      steps {
        sh 'tidy -q -e *.html'
      }
    } 
    stage('Build docker image'){
steps{
  script{
    image = docker.build(registry)
   
  }
}
    }
    stage('Deploy docker image'){
steps{
  script{
       docker.withRegistry('',registryCredential){
      dockerImage.push()
    }  
  }
}
    }
     }
}