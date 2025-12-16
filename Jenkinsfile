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
	    sh 'mvn clean package'
	   }
	 }
	  
   }


}