pipeline {
    agent any
 stages {
  
  stage('Docker Build and Tag') {
           steps {
              
                sh 'docker build -t node-kube-img-scm:latest2 .' 
                sh 'docker tag node-kube-img-scm lijisha27/jenkis-k8s:latest2'
                sh 'docker tag node-kube-img-scm lijisha27/jenkis-k8s:$BUILD_NUMBER'
               
          }
        }
     
  stage('Publish image to Docker Hub') {
          
            steps {
        withDockerRegistry([ credentialsId: "Mydockerhub-credential", url: "" ]) {
          sh  'docker push lijisha27/jenkis-k8s:latest2'
          sh  'docker push lijisha27/jenkis-k8s:$BUILD_NUMBER' 
        }
                  
          }
        }
    stage('Deployment')
{
    steps{
        script{
    sh 'kubectl apply -f nodejsapp-new.yaml'
        }
    }
}
    }
}
