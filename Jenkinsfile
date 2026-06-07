pipeline {
    agent any

    stages {
        stage('Clone repository') {
            steps {
                git url: 'https://github.com/example-user/jenkins-blueocean-demo.git', branch: 'main'
            }
        }

        stage('Build image') {
            steps {
                sh 'docker build -t myapp:latest .'
            }
        }

        stage('Push image') {
            steps {
                withCredentials([usernamePassword(credentialsId: 'dockerhub-creds',
                    usernameVariable: 'DOCKER_USER',
                    passwordVariable: 'DOCKER_PASS')]) {
                    sh '''
                        echo $DOCKER_PASS | docker login -u $DOCKER_USER --password-stdin
                        docker tag myapp:latest example-user/myapp:latest
                        docker push example-user/myapp:latest
                    '''
                }
            }
        }
    }
}
