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
                sh "mvn clean:clean"
                //sh "mvn dependency:copy-dependencies"
                sh "mvn compiler:compile"
            }
        }
        stage('StartWebApp') {
            steps {
                sh "mvn spring-boot:start"
            }
        }
        stage('Package') {
            steps {
                sh "mvn war:war"
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