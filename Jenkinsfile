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
          echo "db password: ${env.DBPASSWORD}"
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
        }
      }
    }
    stage('Deploy') {
      steps {
        sh 'echo ${DB_ENGINE}'
        sh 'echo "Deploy...."'
      }
    }
  }
}
