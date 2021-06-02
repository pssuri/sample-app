/* groovylint-disable-next-line CompileStatic */
pipeline {
    agent any

    stages {
        stage('Cleanup') {
            steps {
                sh 'docker-compose -f docker-compose.yml down'
                sh 'docker rmi -f dockerci_sut dockerci_web'
            }
        }
        stage('Build') {
            steps {
                sh 'docker-compose -f docker-compose.test.yml build'
            }
        }
        stage('Unit test') {
            steps {
                sh 'docker-compose -f docker-compose.test.yml up -d'
            }
        }

        stage('Clean test infra') {
            steps {
                sh 'docker-compose -f docker-compose.test.yml down'
            }
        } 

        stage('Run app') {
            steps {
                sh 'docker-compose -f docker-compose.yml up -d'
            }
        }
    }
}
