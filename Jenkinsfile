node{
   stage('SCM Checkout'){
     git 'https://github.com/iamdeedan/my-app.git'
   }
   stage('Compile-Package'){

      def mvnHome =  tool name: 'maven3', type: 'maven'   
      sh "${mvnHome}/bin/mvn clean package"
	  sh 'mv target/myweb*.war target/newapp.war'
   }
   stage('SonarQube Analysis') {
	        def mvnHome =  tool name: 'maven3', type: 'maven'
	        withSonarQubeEnv('SonarQube') { 
	          sh "${mvnHome}/bin/mvn sonar:sonar"
	        }}
   stage('Build Docker Imager'){
   sh 'docker build -t 231530/myweb:0.0.3 .'
   }
   stage('Docker Image Push'){
   withCredentials([string(credentialsId: '231530', variable: 'dockerPassword')]) {
   sh "docker login -u 231530 -p ${dockerPassword}"
    }
   sh 'docker push 231530/myweb:0.0.3'
   }}
