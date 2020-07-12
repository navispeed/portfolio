
pipeline {
  agent any
//  tools {
//    maven 'maven3'
//    jdk 'jdk14'
//  }
  stages {
    stage('Initialize') {
      steps {
        sh '''
                    echo "PATH = ${PATH}"
                '''
      }
    }

//    stage('Build') {
//      steps {
//        sh 'npm test'
//      }
//      post {
//        success {
//          junit 'target/surefire-reports/**/*.xml'
//        }
//      }
//    }

    stage('Docker') {
      steps {
          script {
            sh 'cp docker/* .'
            docker.withRegistry('http://localhost:32000') {
              def img = docker.build('portfolio')
              img.push()
              img.push("${env.BRANCH_NAME}-${env.BUILD_NUMBER}".replaceAll("/", "-"))
            }
          }
        }
    }
//    stage('Deployment') {
//      steps {
//        build('VideoEditor - CD')
//      }
//    }
  }
}
