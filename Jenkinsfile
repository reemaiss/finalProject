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
    stage('Deploy to AWS'){
      steps{
        withAWS(region:'us-west-2',credentials:'AWS2030rema'){
            sh "pip3 install awscli --upgrade"
            sh "aws --version"
            sh "aws eks --region us-west-2 update-kubeconfig --name myCluster"
            sh 'kubectl apply -f ./deployment.yml'
        }
      }

    }
       
       stage('Staging service'){
         steps{
               withAWS(region:'us-west-2',credentials:'AWS2030rema')  {
                    withCredentials([[$class: 'UsernamePasswordMultiBinding', credentialsId: '2030rema', usernameVariable: 'DOCKER_USERNAME', passwordVariable: 'DOCKER_PASSWORD']]){
                        sh 'docker login -u $DOCKER_USERNAME -p $DOCKER_PASSWORD'
                        sh 'kubectl apply -f ./staging-service.json'
                        sh 'kubectl get pods'
                        sh 'kubectl describe service staginglb'
                    }
                }
         }
       } 
          stage("Cleaning Docker up") {
            steps {
                script {
                    sh "echo 'Cleaning Docker up'"
                    sh "docker system prune"
                }
            }
        }
     }
}
