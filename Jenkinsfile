pipeline {
    agent any
    environment {
        AWS_ACCESS_KEY_ID = credentials('AKIA6KE3AQUXJ6K6ULUH')
        AWS_SECRET_ACCESS_KEY = credentials('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')
        EC2_INSTANCE_ID= 'i-0ac77d907e3fabef8'
    }
    stages {
        stage('Checkout SCM') {
            steps {
                checkout scm
            }
        }
        stage('Build') {
            steps {
                sh 'mvn clean'
                sh 'mvn install'
            }
        }
        stage('Copy WAR to S3') {
            steps {
                sh "aws s3 cp /var/lib/jenkins/workspace/MyFirstProject/target/sysfoo.war s3://mys3-210723/myapp"
            }
        }
        stage('Copy S3 Object to EC2') {
            steps {
                sh "scp -i /path/to/your/private/key /var/lib/jenkins/workspace/MyFirtsProject/target/sysfoo.war ec2-user@${EC2_INSTANCE_ID}:/home/ec2-user/"
            }
        }
    }
}
