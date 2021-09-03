node{
     
    stage('SCM Checkout'){
        git url: 'https://github.com/oktbabs/java-web-app-docker.git',branch: 'develop'
    }
    
    stage(" Maven Clean Package"){
      def mavenHome =  tool name: "Maven382", type: "maven"
      def mavenCMD = "${mavenHome}/bin/mvn"
      sh "${mavenCMD} clean package"
      
    } 
    
    
    stage('Build Docker Image'){
        sh 'docker build -t oktbabs/java-web-app:1.0 .'
    }
    
    stage('Push Docker Image'){
       withCredentials([string(credentialsId: 'Docker_Hub_Pwd', variable: 'Docker_Hub_Pwd')]) {
          sh "docker login -u dockerhandson -p ${Docker_Hub_Pwd}"
        }

        
        sh 'docker push oktbabs/java-web-app:1.0'
     }
     
//      stage('Run Docker Image In Dev Server'){
        
//        def dockerRun = ' docker run  -d -p 8080:8080 --name java-web-app oktbabs/java-web-app'
         
//         sshagent(['DOCKER_SERVER']) {
//          sh 'ssh -o StrictHostKeyChecking=no ubuntu@172.31.20.72 docker stop java-web-app || true'
//          sh 'ssh  ubuntu@172.31.20.72 docker rm java-web-app || true'
//          sh 'ssh  ubuntu@172.31.20.72 docker rmi -f  $(docker images -q) || true'
//          sh "ssh  ubuntu@172.31.20.72 ${dockerRun}"
//      }
       
//    }
     
}
