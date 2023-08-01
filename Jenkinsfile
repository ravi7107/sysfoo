pipeline {
	agent {label "MyFirstProject"}

	stages {
		stage ("This stage will build the package") {
			steps {
				sh "mvn clean"
				sh "mvn install"
			}
		}

		stage ("This stage will copy the package to the S3 bucket") {
			steps {
				sh "aws s3 cp /home/ubuntu//apache-tomcat-9.0.78/webapps s3://mys301082023"
			}
		}
	}
}
