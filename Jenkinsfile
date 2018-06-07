pipeline {
  agent {
    label 'jdk8'
  }
  stages {
    stage('Say Hello') {
      steps {
        echo "Hello ${params.Name}!"
        sh 'java -version'
        echo "Test user name: ${TEST_USER_USR}"
        echo "Test user password: ${TEST_USER_PSW}"
      }
    }
    stage('Testing') {
      failFast true
      parallel {
        stage('Java 8') {
          agent { label 'jkd8' }
          steps {
            sh 'java -version'
            sleep time: 10, unit: 'SECONDS'
          }
        }
        stage('Java 9') {
          agent { label 'jkd9' }       
          steps {
            sh 'java -version'
            sleep time: 20, unit: 'SECONDS'
          }
        }
      }
    }
    stage('Get Kernel') {
      steps {
        script {
          try {
            KERNEL_VERSION = sh (script: "uname -r", returnStdout: true)
          } catch(err) {
            echo "CAUGHT ERROR: ${err}"
            throw err
          }
        }
      }
    }
    stage('Say Kernel') {
      steps {
        echo "${KERNEL_VERSION}"
      }
    }
  }
  environment {
    MY_NAME = 'coldbrew'
    TEST_USER = credentials('test-user')
  }
  parameters {
    string(name: 'Name', defaultValue: 'whoever you are', description: 'To whom should Sir Jenkins say hello?')
  }
  post {
    aborted {
      echo "Why didn't you push my button?"
    }
  }
}
