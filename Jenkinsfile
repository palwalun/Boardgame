pipeline{
 agent any
   environment {
        ACR_LOGIN_SERVER = "devopsproject1.azurecr.io"
        IMAGE_NAME = "boardgame"
        TAG = "latest"
    }
   stages{
     stage('Contiuous Download'){
	   steps{
	    git branch: 'main', url: 'https://github.com/palwalun/Boardgame.git'
	   }
	 }
	 stage('Contiuous Build'){
	   steps{
	    sh 'mvn clean package'
	   }
	 }
	  stage('Build Docker Image'){
	   steps{
	    sh 'docker build -t boardgame:latest . '
	   }
	 }
	 

   }


}