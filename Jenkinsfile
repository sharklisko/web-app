pipeline {
    agent any
    tools {
        go 'go1.16'
    }
    stages {
        stage("clone-project") {
            steps {
                git credentialsId: '', url: 'https://github.com/sharklisko/web-app.git', branch: '**'
            }
        }
        stage("build-app") {
            steps {
                sh 'go mod download'
                sh 'go build -v ./...'
            }
        }
        stage("create-docker-image") {
            steps {
                sh 'docker build -t web-app:v1 .'
            }
        }
        stage("push-docker-image") {
            steps {
                sh 'docker tag web-app:v1 korkmazural/webapp'
                sh 'docker push korkmazural/webapp'
            }
        }
        stage("run-docker-image") {
            steps {
                sh 'docker run web-app:v1'
            }
        }
    }
}