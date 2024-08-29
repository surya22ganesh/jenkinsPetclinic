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
                sh 'trivy fs . > trivyfsoutput.txt'
            }
        }
        stage('tomcat server ssh'){
            steps{
                sshagent(['tomcatserver']) {
                   // some block
                    sh '''
                        echo "from jenkins server"
                        scp -o StrictHostKeyChecking=no . ubuntu@8.117.242.60/home/ubuntu 
                        ssh ubuntu@18.117.242.60 echo "I am from tomcat server"

                    '''
                }
            }
        }
    }
}
