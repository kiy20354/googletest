pipeline {
  agent any
  stages {
    stage('make') {
      steps {
        cmakeBuild(installation: 'InSearchPath', cmakeArgs: './')
      }
    }
  }
}