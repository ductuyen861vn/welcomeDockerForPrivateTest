pipeline {
    agent any

    stages {
        stage('Checkout sc') {
            steps {
                // Checkout sc, branch feature/tuyenpham
                checkout scmGit(branches: [[name: 'feature/TuyenPham']], extensions: [], userRemoteConfigs: [[credentialsId: 'githubTuyenPham', url: 'https://github.com/ductuyen861vn/welcomeDockerForPrivateTest.git']])
            }
        }
        // stage('Build Docker Image') {
        //     steps {
        //         sh 'docker build -t ductuyen861vn/welcomedk . --build-arg HTTP_TIMEOUT=600 --build-arg npm_config_registry=https://registry.yarnpkg.com'
        //     }
        // }
        // stage('Push Docker Image to DockerHub') {
        //     steps {
        //         withCredentials([string(credentialsId: 'dockerHubPWTuyenPham', variable: 'dockerHubPWTuyenPham')]) {
        //             sh 'docker login --username ductuyen861vn --password ${dockerHubPWTuyenPham}'
        //             sh 'docker push ductuyen861vn/welcomedk'
        //         }

        //     }
        // }
        stage('Pull docker image') {
            steps {
                sh 'docker pull ductuyen861vn/welcomedk'
                sh 'docker image ls -a'
                sh 'docker container ls -a'
            }
        }
        stage('Stop the running instance and start new Image') {
            steps {
                sh 'docker stop welcomedk || true && docker rm welcomedk || true && docker rmi ductuyen861vn/welcomedk || true'
                sh 'docker run -d -p 8088:3000 --name welcomedk ductuyen861vn/welcomedk'
                sh 'docker container ls -a'
                sh 'docker inspect -f \'{{range.NetworkSettings.Networks}}{{.IPAddress}}{{end}}\' welcomedk'
            }
        }
    }
}
