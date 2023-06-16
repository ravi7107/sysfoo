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
	}
}
