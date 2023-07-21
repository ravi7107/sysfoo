pipeline {
    agent any
    environment {
        AWS_ACCESS_KEY_ID = credentials('AKIA6KE3AQUXMNPOB6UN').AWS_ACCESS_KEY_ID
        AWS_SECRET_ACCESS_KEY = credentials('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').AWS_SECRET_ACCESS_KEY
        EC2_INSTANCE_IP = '44.203.45.104'
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
                withCredentials([string(credentialsId: 'your-aws-credentials-id', variable: 'AWS_ACCESS_KEY_ID'), string(credentialsId: 'your-aws-credentials-id', variable: 'AWS_SECRET_ACCESS_KEY')]) {
                    sh "aws s3 cp /var/lib/jenkins/workspace/job_4/target/sysfoo.war s3://mys3-210723/myapp"
                }
            }
        }
        stage('Copy S3 Object to EC2') {
            steps {
                withCredentials([string(credentialsId: 'your-aws-credentials-id', variable: 'AWS_ACCESS_KEY_ID'), string(credentialsId: 'your-aws-credentials-id', variable: 'AWS_SECRET_ACCESS_KEY')]) {
                    sh "scp -i /path/to/your/private/key /var/lib/jenkins/workspace/job_4/target/sysfoo.war ec2-user@${EC2_INSTANCE_IP}:/home/ec2-user/"
                }
            }
        }
    }
}
