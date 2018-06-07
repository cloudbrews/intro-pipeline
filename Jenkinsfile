pipeline {
  agent {
    label 'jdk8'
  }
  stages {
    stage('Say Hello') {
      steps {
        echo "Hello ${MY_NAME}!"
        sh 'java -version'
        echo "Test user name: ${TEST_USER_USR}"
        echo "Test user password: ${TEST_USER_PSW}"
      }
    }
  }
  environment {
    MY_NAME = 'coldbrew'
    TEST_USER = credentials('test-user')
  }
}