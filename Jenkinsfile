pipeline {
  agent any
  environment{
    DB_ENGINE = 'mysql'
    DBPASSWORD=credentials('DB_PASSWORD')
  }
  stages {
    stage('Build') {
      steps {
        sh 'echo "Build...."'
        script{
          #echo "db password: ${env.DBPASSWORD}"
          sh 'cd /home/jenkins/onboardingui'
          sh './downloadsrccode.sh'
        }
      }
    }
    stage('Test'){
      steps {
        sh 'echo "Test...."'
        script{
          withCredentials([string(credentialsId:"DB_PASSWORD", variable:"DBPASSWD")]){
            echo "db passwd: ${DBPASSWD}"
          }
          
          sh 'cd /home/jenkins/onboardingui'
          sh 'docker build -f SeleniumTestDockerfile .'
        }
      }
    }
    stage('Deploy') {
      steps {
        sh 'echo ${DB_ENGINE}'
        sh 'echo "Deploy...."'
      }
    }
    
    post{
      always{
        junit '/home/jenkins/onboardingui/onboarding/*.xml'
      }
    }
    
  }
}
