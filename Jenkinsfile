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
     stage ('Check-Git-Secrets') {
      steps {
        sh 'rm trufflehog || true'
        sh 'docker run trufflesecurity/trufflehog --json  https://github.com/adlinsinthiya/webapp.git > trufflehog'
        sh 'cat trufflehog'
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
