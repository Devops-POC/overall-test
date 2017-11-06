node{
	stage ('checkout scm'){
	sh 'git clone https://github.com/Devops-POC/Rest-Assured.git'
	sh 'git clone https://github.com/Devops-POC/pact-test.git'
	sh 'git clone https://github.com/Devops-POC/Jmeter.git'
	sh 'git clone https://github.com/Devops-POC/Cucumber.git'
	sh 'ls -ltr'
	}
	workspace = pwd() 
	stage ('Rest-Assured Test'){
		sh 'cd Rest-Assured'
		def restImage = docker.build("restassured-demo:${env.BUILD_ID}","${workspace}/Rest-Assured")	
		
		sh "docker run -i restassured-demo:${env.BUILD_ID}"
		sh 'docker ps -a | grep \\"restassured-demo:${env.BUILD_ID}\\" | awk \'{ print $1 }\' > outFile'
		containerID = readFile 'outFile'
		echo "The current container id is ${containerID}"
		sh "docker start ${containerID}"
		sh "docker cp ${containerID}:/Rest-Assured/target/surefire-reports/emailable-report.html ."
		sh "cat emailable-report.html"
		sh 'docker images'
		sh "rm -rf Rest-Assured"

        /*restImage.inside {
			sh 'pwd'
			sh 'ls -ltr'	
        }*/
	}

	stage ('PACT Test'){
		sh 'cd pact-test'
		def pactImage = docker.build("pact-demo:${env.BUILD_ID}","${workspace}/pact-test")	
		sh 'docker images'
		sh "rm -rf pact-test"
	}
	stage ('Jmeter Test'){
	sh 'cd Jmeter'
		def jmeterImage = docker.build("jmeter-demo:${env.BUILD_ID}","${workspace}/Jmeter")	
		sh 'docker images'
		sh "rm -rf Jmeter"
	}
	stage ('Cucumber Test'){
	sh 'cd Cucumber'
		def cucumberImage = docker.build("cucumber-demo:${env.BUILD_ID}","${workspace}/Cucumber")	
		sh 'docker images'
		sh "rm -rf Cucumber"
	}
	
	//stage ('clenaup workspace')
	//{
	//sh "rm -rf pact-test Jmeter Cucumber"
	//}
}
