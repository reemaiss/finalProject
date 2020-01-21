pipeline {
  environment {
    registry = "rema2030/finalProject:latest"
    registryCredential = 'dockerhub'
  }


     agent any 
     stages {

        stage('Lint HTML') {
      steps {
        sh 'tidy -q -e *.html'
      }
    }   
  


     }
}