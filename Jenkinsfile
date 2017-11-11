pipeline {
  agent any
  stages {
    stage('Init') {
      steps {
        sh 'git submodule update --init'
      }
    }
    stage('Build') {
      steps {
        sh '''mkdir -p build
cd build'''
        deleteDir()
        sh '''cmake ..
make -j16'''
      }
    }
    stage('Regression Tests') {
      steps {
        sh '''cd build
ctest -VV'''
      }
    }
    stage('Deploy') {
      steps {
        echo 'Pipleline finished.'
        cleanWs(cleanWhenAborted: true, cleanWhenNotBuilt: true, cleanWhenSuccess: true)
      }
    }
  }
}