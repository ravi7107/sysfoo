pipeline {
	agent any

	stages {
		stage ("Build the package") {
			steps {
				node ("build_server") {
					print ("Clone the git repo")
					checkout scm

					print ("Building the war package")
					sh "mvn install"

					print ("Stash the package")
					stash ( includes: "target/hello-world-web-app.war", name: "package")
				}
			}
		}
		stage ("Deploy the package") {
			steps {
				node ("deploy_server") {
					print ("Unstash the package")
					unstash (name: "package")

					print ("Delete the old package if present")
					sh "rm -rf /usr/local/tomcat/webapps/hello-world-web-app.war"

					print ("Copy the new package")
					sh "cp /app/build_server/workspace/declarative_pipeline_example/target/hello-world-web-app.war /usr/local/tomcat/webapps/"
				}
			}
		}
	}
	post {
		Failure:
	}
}
}
