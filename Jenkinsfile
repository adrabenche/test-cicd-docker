pipeline {
  agent any
  stages {
    stage('Build') {
      steps {
        sh "docker build -t ${env.RepoDockerHub}/${env.NameContainer}:${env.BUILD_NUMBER} ."
      }
    }

    stage('Run') {
      steps {
        sh "docker run -p 400${env.BUILD_NUMBER}:3000 -d --name nodeapp_test${env.BUILD_NUMBER} ${env.RepoDockerHub}/${env.NameContainer}:${env.BUILD_NUMBER}"
        // sh "docker run --rm -p 400${env.BUILD_NUMBER}:3000 -d --name nodeapp_test${env.BUILD_NUMBER} ${env.RepoDockerHub}/${env.NameContainer}:${env.BUILD_NUMBER}"
      }
    }

    stage('CI') {
      steps {
        sh 'echo "hola mundo"'
      }
    }

    stage('Stop containers') {
      steps {
        sh "docker stop nodeapp_test${env.BUILD_NUMBER}"
      }
    }

    // stage('Clean dangling images') {
    //   steps {
    //     sh "docker rmi ${env.RepoDockerHub}/${env.NameContainer}:${env.BUILD_NUMBER}"
    //   }
    // }


    // stage('Login to Dockerhub') {
    //   steps {
    //     sh "echo $Dockerhub_Credentials_PSW | docker login -u $Dockerhub_Credentials_USR --password-stdin"
    //   }
    // }

    // stage('Push image to Dockerhub') {
    //   steps {
    //     sh "docker push ${env.RepoDockerHub}/${env.NameContainer}:${env.BUILD_NUMBER}"
    //   }
    // }

  }
  environment {
    RepoDockerHub = 'adrabencheeduit'
    NameContainer = 'nodeapp_edit'
    // Dockerhub_Credentials = credentials('docker-user')
  }
}
