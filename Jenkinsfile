pipeline {
    agent any

    tools {
        maven 'Maven-3'
    }

    stages {

        stage('Build') {
            steps {
                bat 'clean package'
            }
        }

        stage('Deploy to EC2') {
            steps {
                sshagent(['ec2-ssh-key']) {
                    bat '''
                    ssh -o StrictHostKeyChecking=no ec2-user@44.195.85.219 "pkill -f java || true"
                    scp -o StrictHostKeyChecking=no target/*.jar ec2-user@44.195.85.219:/home/ec2-user/app.jar
                    ssh -o StrictHostKeyChecking=no ec2-user@44.195.85.219 "nohup java -jar /home/ec2-user/app.jar > output.log 2>&1 &"
                    '''
                }
            }
        }
    }
}