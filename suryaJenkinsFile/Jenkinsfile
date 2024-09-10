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
        stage ('rename maven build package'){
            steps{
                sh ''' 
                    cd target
                    mv *.war surya.war
                '''
            }
        }
        stage('tomcat server ssh'){
            steps{
                sshagent(['tomcatserver']) {
                   // some block
                    sh '''
                        ssh -tt ubuntu@8.117.242.60 -o StrictHostKeyChecking=no 
                        ssh ubuntu@8.117.242.60 echo tomcat agent added
                        scp target/surya.war ubuntu@8.117.242.60:/opt
                    '''
                }
            }
        }
    }
}

                        // scp -o StrictHostKeyChecking=no target/surya.war ubuntu@8.117.242.60:/opt
                        // echo "from jenkins server"
                        // pwd
                        // ssh -tt -o StrictHostKeyChecking=no ubuntu@8.117.242.60
                        // scp target/surya.war ubuntu@8.117.242.60:/opt