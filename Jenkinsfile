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
//         sh 'docker run gesellix/trufflehog --json https://github.com/Siddeshwarsid/webapp.git > trufflehog'
//         sh 'cat trufflehog'
//       }
//     }
     stage ('owasp') {
       steps {
         sh 'rm owasp* || true'
         sh 'wget "https://raw.githubusercontent.com/Siddeshwarsid/webapp/master/owasp-dependency-check.sh" '
         sh 'chmod +x owasp-dependency-check.sh'
         sh 'bash owasp-dependency-check.sh'
         sh 'cat /var/lib/jenkins/OWASP-Dependency-Check/reports/dependency-check-report.xml'
       }
       
     }
        stage('UNIT TEST'){
            steps {
                sh 'mvn test'
            }
        }

        stage('INTEGRATION TEST'){
            steps {
                sh 'mvn verify -DskipUnitTests'
            }
        }

        stage ('CODE ANALYSIS WITH CHECKSTYLE'){
            steps {
                sh 'mvn checkstyle:checkstyle'
            }
            post {
                success {
                    echo 'Generated Analysis Result'
                }
            }
        }

     
     stage('sonarQube') {
       steps {
         withSonarQubeEnv('sonar') {
           sh 'mvn sonar:sonar'
           sh 'cat target/sonar/report-task.txt'
         }
       }
     }
     
    stage('build') {
      steps {
        sh 'mvn clean package'
      }
    }
     
     stage('deploy to tomcat') {
       steps {
         sshagent(['tomcat']) {
           sh 'scp -o StrictHostKeyChecking=no target/*.war ubuntu@52.70.102.174:/prod/apache-tomcat-8.5.81/webapps/webapp.war'
         }
       }
    }
    
  }
}
