node{
    def mvnHome = tool name:'Maven 3.6.1', type:'maven'
   properties([buildDiscarder(logRotator(artifactDaysToKeepStr: '', artifactNumToKeepStr: '', daysToKeepStr: '', numToKeepStr: '5'))])
    
    stage('checkout'){
      git credentialsId: '27d8f6b0-5183-4edb-9d7f-590e8c14d0e1', url: 'https://github.com/revathigajendiran/maven-web-application.git'  
    }
    stage('build'){
        sh "${mvnHome}/bin/mvn clean package"
    }
    stage('codequality'){
        sh "${mvnHome}/bin/mvn sonar:sonar"
    }
    stage('codeuplaodartifactory'){
        sh "${mvnHome}/bin/mvn clean deploy"
    }
    stage('deployappserver'){
        /*sshagent(['tomcat-server']) {
      sh 'cp $workspace/target/*.war ec2-user@13.235.90.135:cd/opt/apache-tomcat-9.0.21/webapps/'
}*/
         sh 'cp $WORKSPACE/target/*.war /opt/apache-tomcat-9.0.21/webapps/maven-web-application.war'
    }
    /*stage('mailconfig'){
mail bcc: '', body: 'Build is over', cc: 'revathimcaharish@gmail.com', from: '', replyTo: '', subject: 'Mail Checking', to: 'revathimcaharish@gmail.com'    }*/
}
