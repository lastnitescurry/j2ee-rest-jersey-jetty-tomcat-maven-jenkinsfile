node {
	// Mark the code checkout 'stage'....
	stage 'Checkout'
	
	// Get some code from a GitHub repository
	git 'https://github.com/lastnitescurry/j2ee-rest-jersey-jetty-tomcat-maven-jenkinsfile.git'
	
	// Get the maven tool.
	// ** NOTE: This 'M3' maven tool must be configured
	// **       in the global configuration.           
	def mvnHome = tool 'M3'
	
	// Mark the code build 'stage'....
	stage 'Build'
	// Run the maven build
	bat "${mvnHome}/bin/mvn -Dmaven.test.failure.ignore clean package"
	//step([$class: 'JUnitResultArchiver', testResults: '**/target/surefire-reports/TEST-*.xml'])
	
	stage 'Demo in Telford'
	input 'What the heck?'

	   // Mark the code build 'stage'....
	stage 'Archive'
	stash includes: 'target/*.war', name: 'RESTful.war'
	
	stage 'Release To Manual Test'
	input 'Deploy to local Tomcat?'
	
	stage 'Deploy To Manual Test'
	unstash 'RESTful.war'
	bat 'copy target\\*.war F:\\Apps\\Tomcat\\apache-tomcat-8.5.4\\webapps'
   
	stage 'SonarQube Analysis'
	bat "${mvnHome}/bin/mvn -Dmaven.test.failure.ignore sonar:sonar"

	stage 'Release To Production'
	input 'Free the bird? Let the birdy fly'

}