pipeline{
  agent any
  tools {
    maven 'maven-3.6.1'
  }
   stages {
//     stage('Initialize') {
//       steps {
//         sh '''
//             echo "PATH = ${PATH}"
//             echo "M2_HOME = ${M2_HOME}"
//            '''
//       }
//     }
    
    stage('build') {
      steps {
        sh 'mvn clean package'
      }
    }
     stage('deploy to tomcat') {
       steps {
         sshagent(['tomcat']) {
           sh 'scp StrictHostKeyChecking=no target/*.war ubuntu@34.238.85.6:/prod/apache-tomcat-8.5.81/webapps/webapp.war'
         }
       }
    }
    
  }
}
    
