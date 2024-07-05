pipeline {
  agent any

  stages {
      stage('Build Artifact') {
            steps {
              sh "mvn clean package -DskipTests=true" // Test1
              archive 'target/*.jar' 
            }
        }   
    }
}
