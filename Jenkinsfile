pipeline {
  agent any
  stages {
    stage('Init') {
      steps {
        sh 'git submodule update --init'
      }
    }
    stage('Build') {
      parallel {
        stage('Setup') {
          steps {
            sh '''mkdir build
cd build'''
          }
        }
        stage('Cmake') {
          steps {
            sh 'cmake ..'
          }
        }
        stage('Make') {
          steps {
            sh 'make -j16'
          }
        }
      }
    }
    stage('Unit Tests') {
      steps {
        sh './bin/unit_test'
      }
    }
    stage('Regression Tests') {
      steps {
        sh '''cd examples
ctest -VV'''
      }
    }
    stage('Deploy') {
      steps {
        echo 'Pipleline finished.'
      }
    }
  }
}