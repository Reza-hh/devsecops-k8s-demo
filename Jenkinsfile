pipeline {
  agent any

  stages {
      stage('Build Artifact') {
            steps {
              sh "mvn clean package -DskipTests=true" 
              archive 'target/*.jar' 
            }
        }   
    }

  stages {
      stage('docker Build Push') {
            steps {
                withDockerRegistry([credentialId: "docker-hub", url:""]) {
                    sh 'printenv' 
                    sh 'docker build -t siddharth/numeric-app""$GIT_COMMIT"" .'
                }
            }
        }   
    stage('Kubernetes Deployment - Dev') {
            steps {
                withKubeConfig([credentialsId: "kubeconfig"]) {
                sh "sed -i s#replace#siddharth67/numeric-app:${GIT_COMMIT}#g' k8s_deployment_service.yaml" 
                sh "kubectl apply -f k8s_deployment_service.yaml"
                }
            }
        }   
    }
}
