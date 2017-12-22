/*pipeline {
  agent any
  stages {
    stage('first stage') {
      parallel {
        stage('first stage') {
          steps {
            echo 'Hola caracola'
          }
        }
        stage('hola') {
          steps {
            echo 'ffdfd'
          }
        }
      }
    }
    checkpoint 'dddd'
    stage('second stage') {

       
          steps {
            checkpoint 'dddd'
          }
       
      
    }
    stage('third stage') {
      parallel {
        stage('third stage') {
          steps {
            ws(dir: 'sss')
          }
        }
        stage('error') {
          steps {
            sh 'sh "echo \'adios\'"'
          }
        }
      }
    }
  }
  options {
    skipDefaultCheckout()
  }
}
*/
pipeline {
  agent {
    node {
      docker.label('jenkins-java')
    }
  }
  stages {
    stage('CI') {
      steps {
        sh 'ls -al'
        sh "cd ${env.WORKSPACE}"
        sh 'ls -al'
      }
    }
  }
}

