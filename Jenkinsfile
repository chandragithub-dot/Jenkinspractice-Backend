pipeline {
    agent any

    stages {

        stage('Build') {
            steps {
                bat 'mvnw.cmd clean package'
            }
        }
        stage('Deploy to EC2') {
    steps {
        bat """
        scp -i C:\\Users\\bhush\\Desktop\\employeeMS.pem target\\employeemanagmentbackend-0.0.1-SNAPSHOT.jar ec2-user@44.195.85.219:/home/ec2-user/
        
        ssh -i C:\\Users\\bhush\\Desktop\\employeeMS.pem ec2-user@44.195.85.219 ^
        "pkill -f employeemanagmentbackend || true && nohup java -jar /home/ec2-user/employeemanagmentbackend-0.0.1-SNAPSHOT.jar > app.log 2>&1 &"
        """
    }
}
    }
}