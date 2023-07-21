pipeline {
    agent any

    environment {
        S3_BUCKET = "mys3-210723"
        S3_OBJECT_KEY = "sysfoo.war"
        EC2_INSTANCE_IP = "i-0e66df3fdf719eba4"
        EC2_INSTANCE_USER = "ravi"
        EC2_INSTANCE_PATH = "/var/lib/jenkins/workspace/Job_4/target/sysfoo.war"
    }

    stages {
        stage('Build') {
            steps {
                // Checkout your source code from version control (e.g., Git)
                checkout scm

                // Build your project using Maven
                sh 'mvn clean'
                sh 'mvn install'
            }
        }

        stage('Copy WAR to S3') {
            steps {
                // Copy the generated WAR file to S3
                sh "aws s3 cp /var/lib/jenkins/workspace/Job_4/target/sysfoo.war s3://${S3_BUCKET}/${S3_OBJECT_KEY}"
            }
        }

        stage('Copy S3 Object to EC2') {
            steps {
                // Copy the WAR file from S3 to EC2 instance
                sh "scp -i /home/ubuntu s3://${S3_BUCKET}/${S3_OBJECT_KEY} ${EC2_INSTANCE_USER}@${EC2_INSTANCE_IP}:${EC2_INSTANCE_PATH}"
            }
        }
    }
}
