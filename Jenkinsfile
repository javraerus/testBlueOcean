pipeline {
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
    stage('second stage') {

        stage('check') {
          steps {
            checkpoint 'dddd'
          }
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
