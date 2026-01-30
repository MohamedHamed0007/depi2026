pipeline {
    agent any
    environment {
        GH = credentials('github')
        DOCKER = credentials('docker')
        APP_VERSION = "V1.2.0"
    }
    stages {
        stage("checkout code") {
            steps {
                checkout scmGit(branches: [[name: '*/main']], extensions: [], userRemoteConfigs: [[credentialsId: 'github', url: 'https://github.com/abobakryousre/depi2026.git']])
                sh 'ls -l'

            }
        }
        stage("Build"){
            steps {
                echo "running build ..."
            }
        }
        stage("test"){
            steps{
                echo "running test ..."
            }
        }
          stage("Release ") {
            steps {
                withCredentials([usernamePassword(credentialsId: 'docker', passwordVariable: 'dockerPassword', usernameVariable: 'dockerUser')]) {
            
                    sh 'echo $dockerPassword | docker login -u $dockerUser --password-stdin'
                    echo "build docker image"
                    sh 'docker build . -t abobakryousre/depi:$APP_VERSION'
                    echo "push image docker hub"
                    sh 'docker push abobakryousre/depi:$APP_VERSION'
                }

                
               

            }
        }
        stage("deploy"){
            steps {
                input message: 'do you want to deploy?', ok: 'okay, Deploy'
                sh 'echo Deploying...'
            }
        }
    
    }
    post {
        success {
            echo "Pipeline success"
        }
        
    }
  
}
