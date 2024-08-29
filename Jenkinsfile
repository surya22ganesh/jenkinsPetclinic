pipeline {
    agent any

    stages {
        stage('Hello') {
            steps {
                echo 'Hello World'
            }
        }
        stage('maven build'){
            sh 'mvn clean package'
        }
        stage('trivy fs scan'){
            sh 'trivy fs .'
        }
    }
}
