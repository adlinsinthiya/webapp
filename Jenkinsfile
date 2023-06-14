pipeline{
agent any
tools{
maven 'Maven'
}
stages{
  stage(initialize){
  sh '''
          echo "Path =${Path}"
          echo "M2_Home= ${M2_Home}"
     '''
  }
  stage('Build')
  {
     sh 'mvn clean package'
  }
}
}
