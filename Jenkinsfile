pipeline {
    agent any

    stages {
        stage('GetProject') {
            steps {
                git 'https://github.com/MT-byte/springboot_demo'
            }
        }
        stage('Build') {
            steps {
                sh 'mvn clean:clean'
                sh 'mvn dependency:copy-dependencies'
                sh 'mvn compiler:compile'
            }
        }
        stage('StartWebApp') {
            steps {
                sh 'ls'
                //sh 'mvn spring-boot:start'
            }
        }
        stage('Package') {
            steps {
                sh 'mvn war:war'
            }
        }
        stage('Deploy') {
            steps {
                sh 'docker build -f Dockerfile -t myapp . '
                sh 'docker rm -f "myappcontainer" || true'
                sh 'docker run --name "myappcontainer" -p 8081:8080 --detach myapp:latest'
            }
        }
    }

    post {
        success {
            archiveArtifacts allowEmptyArchive: true,
            artifacts: '**/demo*.war'
        }
    }
}