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
            sh 'sh "echo \'hola\'"'
          }
        }
      }
    }
    stage('second stage') {
      parallel {
        stage('second stage') {
          steps {
            echo 'This time, the Maven version should be 3.3.9'
            checkpoint 'Completed tests'
          }
        }
        stage('check') {
          steps {
            sh 'sh "echo \'hola\'"'
          }
        }
      }
    }
    stage('third stage') {
      parallel {
        stage('third stage') {
          steps {
            sh kjhkjhkjh
          }
        }
        stage('') {
          steps {
            sh 'sh "echo \'adios\'"'
          }
        }
      }
    }
  }
}