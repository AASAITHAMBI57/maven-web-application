node{

    def mavenHome = tool name: "maven3.9.7"

    // Checkout Stage
    stage('Checkout Code'){
        git branch: 'development', credentialsId: 'git-pass', url: 'https://github.com/AASAITHAMBI57/maven-web-application.git'
    }

    // Build Stage
    stage('Maven Build'){
        sh"${mavenHome}/bin/mvn clean package"
    }

    // SonerReport Stage
    stage('ExecuteSonarQubeReport'){
        sh"${mavenHome}/bin/mvn sonar:sonar"
    }

    // UploadArtifactsIntoNexus
    stage('UploadArtifactsIntoNexus'){
        sh"${mavenHome}/bin/mvn deploy"
    }

    stage('Deploy to Tomcatserver'){
        sshagent(['a685cf36-acee-4fd0-b4e2-69f5af86cb28']) {
            sh"scp -o StrictHostKeyChecking=no target/maven-web-application.war ec2-user@172.31.6.87:/opt/apache-tomcat-9.0.89/webapps"
        }
    }

}//Node closing
