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
                  docker build -t siddharth67/numeric-app:my_app  
             # sh 'docker push siddharth67/numeric-app:""$GIT_COMMIT""' 
            }
        }   
    }
}
