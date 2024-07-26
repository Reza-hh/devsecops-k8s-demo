pipeline {
  agent any

  stages {
      stage('Build Artifact') {
            steps {
              sh "mvn clean package -DskipTests=true" 
              archive 'target/*.jar' 
            }
        } 
    stage('SonarQube - SAST') {
            steps {
              
               sh "mvn clean verify sonar:sonar -Dsonar.projectKey=numeric-application -Dsonar.projectName='numeric-application' -Dsonar.host.url=http://192.168.50.161:9000 -Dsonar.token=sqp_0dd138ae4bbee1bab120f783f22a7073e2a6314a"
                
            }
        }
    

    
      stage('Kubernetes Deployment -Dev') {
            steps {
               withKubeConfig([credentialsId: 'kubeconfig']) {
               sh "sed -i 's#replace#siddharth67/numeric-app:${GIT_COMMIT}#g' k8s_deployment_service.yaml"
               sh "kubectl apply -f k8s_deployment_service.yaml" 
            }
        }
      
    }
 }
}



