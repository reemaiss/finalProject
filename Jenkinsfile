pipeline {
  environment {
    registry = "rema2030/api:latest"
    registryCredential = 'rema2030'
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
    image = docker.build(registry)
    docker.withRegistry('',registryCredential){
      dockerImage.push()
    }  
  }
}
    }
     }
}