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
              sh 'docker build -t siddharth67/numeric-app:""$Git_COMMT"" .' 
              sh 'docker push siddharth67/numeric-app:""$GIT_COMMT""'
            }
        }   
    }
}
