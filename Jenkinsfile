pipeline {
    agent any
	
	  tools
    {
       maven "maven"
    }
 stages {
      stage('checkout') {
           steps {
             
                git branch: 'master', url: 'https://github.com/srikanta1219/CI-CD-using-Docker-master.git'
             
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
                //sh 'docker tag samplewebapp srikanta1219/samplewebapp:latest'
                sh 'docker tag samplewebapp srikanta1219/samplewebapp:$BUILD_NUMBER'
               
          }
        }
     
  stage('Publish image to Docker Hub') {
          
            steps {
				withDockerRegistry([ credentialsId: "DockerHub", url: "" ]) {
			//	sh  'docker push srikanta1219/samplewebapp:latest'
				sh  'docker push srikanta1219/samplewebapp:$BUILD_NUMBER' 
        }
                  
          }
        }  
    }
	}
    
