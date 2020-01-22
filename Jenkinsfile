pipeline {
  environment {
    registry = "2030rema/api:latest"
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
    dockerImage = docker.build(registry)
    docker.withRegistry('',registryCredential){
      dockerImage.push()
    }  
  }
}
    }
    stage('Upload to AWS'){
      steps{
        withAWS(region:'us-east-2',credentials:'remaAWSS')
        sh "aws eks --region us-east-2 update-kubeconfig --name myCluster"
                    sh 'kubectl apply -f ./deployment.yml'
      }

    }
     }
}