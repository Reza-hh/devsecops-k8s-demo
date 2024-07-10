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
              sh 'printenv' 
              sh 'docker build -t siddharth/numeric-app""$GIT_COMMIT"" .'
            }
        }   
    }
}
