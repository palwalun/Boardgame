pipeline{
 agent any
   environment {
        ACR_LOGIN_SERVER = "devopsproject2.azurecr.io"
        IMAGE_NAME = "boardgame-app"
        TAG = "latest"
    }
   stages{
     stage('Checkout'){
	   steps{
	    checkout scm
	   }
	 }
	 stage('Contiuous Build'){
	   steps{
	    sh 'mvn clean package'
	   }
	 }
	  stage('Build Docker Image'){
	   steps{
	    sh 'docker build -t boardgame-app:latest . '
	   }
	 }
	 stage('Login to ACR') {
       steps {
         withCredentials([usernamePassword(
             credentialsId: 'acr-creds',
             usernameVariable: 'ACR_USER',
             passwordVariable: 'ACR_PASS'
         )]) {
             sh '''
               echo $ACR_PASS | docker login $ACR_LOGIN_SERVER \
               -u $ACR_USER --password-stdin
             '''
         }
       }
     }
	 stage('Tag Image') {
     steps {
        sh '''
          docker tag ${IMAGE_NAME}:${TAG} \
          $ACR_LOGIN_SERVER/${IMAGE_NAME}:${TAG}
        '''
         }
       }
	 stage('Push Image to ACR'){
	   steps{
	    sh 'docker push $ACR_LOGIN_SERVER/${IMAGE_NAME}:${TAG}'
	    }
	   }
	 stage('Deploy to k8s cluster'){
	  steps{
	   sh '''
	    kubectl apply -f boardgame-deployment.yml
		  kubectl apply -f service.yml
		'''
	   }
	  
	 }



  }
}