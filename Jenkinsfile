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
                        ssh ubuntu@8.117.242.60 -o StrictHostKeyChecking=no 
                        ssh ubuntu@8.117.242.60 echo tomcat agent added
                        scp target/myweb.war ubuntu@8.117.242.60:/opt/
                        // ssh ubuntu@8.117.242.60 /opt/apache10/bin/shutdown.sh
                        // ssh ubuntu@8.117.242.60 /opt/apache10/bin/startup.sh
                  '''
                }
            }
        }
    }
}
