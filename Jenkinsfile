pipeline {
	agent {label "build_server"}

	stages {
		stage ("This stage will build the package") {
			steps {
				sh "mvn clean"
				sh "mvn install"
			}
		}

		stage ("This stage will copy the package to the S3 bucket") {
			steps {
				sh "aws s3 cp /home/ubuntu/build_server/workspace/Asignment-1/target/sysfoo.war s3://mybucket160623"
			}
		}

		 stage('Copy S3 file to EC2') {
            steps {
                script {
                    def bucketName = "mybucket160623"
                    def key = "sysfoo.war"
                    def destinationPath = "/tomcat/apache-tomcat-10.1.10/webapps/sysfoo.war"
                    def instanceId = "i-00ec35d1dccce899c"  // Replace with your EC2 instance ID
                    
                    // Step 3: Copy S3 file to EC2 instance using SCP
                    sh "aws s3 cp s3://${bucketName}/${key} ec2-user@${instanceId}:${destinationPath}"
                }
            }
	}
}
}
