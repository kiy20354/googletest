pipeline {
  agent any
  stages {
    stage('make') {
      steps {
        cmake(installation: 'InSearchPath', arguments: './')
      }
    }
  }
}