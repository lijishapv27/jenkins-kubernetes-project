pipeline {
    agent any
 stages {
  
  stage('Docker Build and Tag') {
           steps {
              
                sh 'docker build -t node-kube-img:latest .' 
                sh 'docker tag node-kube-img lijisha27/jenkis-k8s:latest'
                sh 'docker tag node-kube-img lijisha27/jenkis-k8s:$BUILD_NUMBER'
               
          }
        }
     
  stage('Publish image to Docker Hub') {
          
            steps {
        withDockerRegistry([ credentialsId: "Mydockerhub-credential", url: "" ]) {
          sh  'docker push lijisha27/jenkis-k8s:latest'
          sh  'docker push lijisha27/jenkis-k8s:$BUILD_NUMBER' 
        }
                  
          }
        }
    stage('Deployment')
{
    steps{
        script{
    sh 'kubectl apply -f nodejsapp.yaml'
        }
    }
}
    }
}
