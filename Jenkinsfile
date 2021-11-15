pipeline {
    agent any
	
	  tools
    {
       maven "Maven"
    }
 stages {
      stage('checkout') {
           steps {
             
                git credentialsId: 'git', url: 'https://github.com/ravinder-sin/Final1.git'
             
          }
        }
	 stage('Execute Maven') {
           steps {
             
                sh 'mvn package'             
          }
        }
        

  stage('Docker Build and Tag') {
           steps {
              
                sh 'docker build -t samplewebapp:latest .' 
                sh 'docker tag samplewebapp srinku28/samplewebapp:latest'
                //sh 'docker tag samplewebapp srinku28/samplewebapp:$BUILD_NUMBER'
               
          }
        }
     
  stage('Publish image to Docker Hub') {
          
            steps {
        withDockerRegistry(credentialsId: 'dockerhub', url: '') {
		sh 'docker push srinku28/samplewebapp'
    // some block
            }
                  
          }
        }
     
      stage('Run Docker container on Jenkins Agent') {
             
            steps 
			{
                sh "docker run -d -p 84:8080 srinku28/samplewebapp"
 
            }
        }
 
    }
	}
    
