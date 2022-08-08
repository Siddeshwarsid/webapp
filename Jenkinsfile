pipeline{
  agent any
  tools {
    maven 'Maven'
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
//     stage ('Check-Git-Secrets') {
//       steps {
//         sh 'rm trufflehog || true'
//         sh 'docker run gesellix/trufflehog --json https://github.com/cehkunal/webapp.git > trufflehog'
//         sh 'cat trufflehog'
//       }
//     }    
    stage('build') {
      steps {
        sh 'mvn clean package'
      }
    }
//      stage('deploy to tomcat') {
//        steps {
//          sshagent(['tomcat']) {
//            sh 'scp -o StrictHostKeyChecking=no target/*.war ubuntu@52.90.52.15:/prod/apache-tomcat-8.5.81/webapps/webapp.war'
//          }
//        }
//     }
    
  }
}
    
