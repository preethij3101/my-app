node{
   stage('SCM Checkout'){
     git 'https://github.com/preethij3101/my-app.git'
   }
   stage('Maven - Build Stage'){

      def mvnHome =  tool name: 'maven3', type: 'maven'   
      sh "${mvnHome}/bin/mvn clean package"
	  sh 'mv target/myweb*.war target/newapp.war'
   }
   stage('Build Docker Image'){
   sh 'docker build -t sulthanaa/myweb:0.0.2 .'
  }
  stage('Docker Image Push'){
   withCredentials([string(credentialsId: 'docker123', variable: 'dockerPassword')]) {
   sh "docker login -u sulthanaa -p ${dockerPassword}"
    }
   sh 'docker push sulthanaa/myweb:0.0.2'
   }
   stage('Docker deployment'){
   sh 'docker run -d -p 8090:8080 --name tomcattest sulthanaa/myweb:0.0.2' 
   }  
}
