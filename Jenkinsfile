pipeline{
 agent any
   stages{
     stage('Contiuous Download'){
	   steps{
	    git branch: 'main', url: 'https://github.com/palwalun/Boardgame.git'
	   }
	 }
	 stage('Contiuous Build'){
	   steps{
	   dir
	    sh 'mvn clean package'
	   }
	 }
	  stage('Build Docker Image'){
	   steps{
	   dir
	    sh 'docker build -t boardgame:latest . '
	   }
	 }
   }


}