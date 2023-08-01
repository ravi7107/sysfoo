pipeline {
    agent any
    environment {
        AWS_ACCESS_KEY_ID = 'credentials('AKIA6KE3AQUXE5HQCUMN').AWS_ACCESS_KEY_ID'
        AWS_SECRET_ACCESS_KEY = 'credentials('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').AWS_SECRET_ACCESS_KEY'
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
                withCredentials([string(credentialsId: 'AKIA6KE3AQUXE5HQCUMN', variable: 'AWS_ACCESS_KEY_ID'), string(credentialsId: '5yFrnIg8TNFcEV46i7Gh1kWfda4BcEKhTnJ30ml2', variable: 'AWS_SECRET_ACCESS_KEY')]) {
                    sh "aws s3 cp /var/lib/jenkins/workspace/job_4/target/sysfoo.war s3://mys3-210723/myapp"
                }
            }
        }
        stage('Copy S3 Object to EC2') {
            steps {
                withCredentials([string(credentialsId: 'AKIA6KE3AQUXE5HQCUMN', variable: 'AWS_ACCESS_KEY_ID'), string(credentialsId: '5yFrnIg8TNFcEV46i7Gh1kWfda4BcEKhTnJ30ml2', variable: 'AWS_SECRET_ACCESS_KEY')]) {
                    sh "scp -i /path/to/your/private/key /var/lib/jenkins/workspace/MyFirtsProject/target/sysfoo.war ec2-user@${EC2_INSTANCE_ID}:/home/ec2-user/"
                }
            }
        }
    }
}
