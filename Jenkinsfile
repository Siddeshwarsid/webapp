pipeline{
  agent any
  tools {
    maven 'maven-3.6.1'
  }
  stages {
    stage('Initialize') {
      steps {
        sh '''
            echo "PATH = ${PATH}"
            echo "M2_HOME = ${M2_HOME}"
           '''
      }
    }
    
    stage('build') {
      steps {
        sh 'mvn clean package'
      }
    }
    
  }
}
    
