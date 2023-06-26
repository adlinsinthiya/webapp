pipeline {
  agent any 
  tools {
    maven 'Maven'
  }
  stages {
    stage ('Initialize') {
      steps {
        sh '''
                    echo "PATH = ${PATH}"
                    echo "M2_HOME = ${M2_HOME}"
            ''' 
      }
    }
 stage ('Build') {
      steps {
      sh 'mvn clean package'
       }
    }
    stage ('Deploy-To-Tomcat') {
            steps {
           sshagent(['Tomcat-Server-Agent']) {
                sh 'scp -o StrictHostKeyChecking=no target/*.war ubuntu@54.152.109.190:/prod/apache-tomcat-9.0.76/webapps/webapp.war'
              }      
           }       
    }
}
}
