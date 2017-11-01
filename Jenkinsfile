node{
	stage ('checkout scm'){
	sh 'git clone https://github.com/Devops-POC/Rest-Assured.git'
	sh 'git clone https://github.com/Devops-POC/pact-test.git'
	sh 'ls -ltr'
	}
	workspace = pwd() 
	stage ('Rest-Assured Test'){
		sh 'cd Rest-Assured'
		def restImage = docker.build("restassured-demo:${env.BUILD_ID}","${workspace}/Rest-Assured")	
		sh 'docker images'
        /*restImage.inside {
			sh 'pwd'
			sh 'ls -ltr'	
        }*/
	}

	stage ('PACT Test'){
	}
	stage ('Jmeter Test'){
	}
	
	stage ('clenaup workspace')
	{
	sh "rm -rf pact-test Rest-Assured"
	}
}
	
    