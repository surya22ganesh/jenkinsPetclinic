pipeline {
    agent any

    stages {
        stage('Hello') {
            steps {
                echo 'Hello World'
            }
        }
        stage('maven build'){
            steps {
                sh 'mvn clean package'
            }
        }
        stage('trivy fs scan'){
            steps {
                sh 'trivy fs .'
            }
        }
    }
}
