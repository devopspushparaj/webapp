pipeline {
    agent any
    tools {
        maven 'Maven'
    }

    stages {
        stage('Intialize') {
            steps {
            sh '''
                    echo "PATH = ${PATH}"
                    echo "M2_HOME = ${M2_HOME}"
               ''' 
            }
        }
        stage('Build') {
            steps {
            sh 'mvn clean package'
            }
        }
        stage ('Deploy-To-Tomcat') {
            steps {
              sshagent(['tomcat']) {
                sh 'scp -o StrictHostKeyChecking=no /home/ubuntu/webapp/target/WebApp.war ubuntu@3.108.62.198:/home/ubuntu/prod/apache-tomcat-8.5.69/webapps/webapp.war'
               }      
          }       
      }
    }
}
