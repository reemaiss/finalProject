pipeline {
  environment {
    registry = "2030rema/api:latest"
    registryCredential = '2030rema'
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
    dockerImage = docker.build(registry)
    docker.withRegistry('',registryCredential){
      dockerImage.push()
    }  
  }
}
    }
    stage('DEPLOY to AWS'){
      steps{
        withAWS(credentials:'AWS2030rema',region:'us-east-2'){
            sh "aws eks --region us-east-2 update-kubeconfig --name myCluster"
            sh 'kubectl apply -f ./deployment.yml'
        }
      }

    }
     }
}
