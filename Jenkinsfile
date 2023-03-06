node{

    stage('git clone'){
    git credentialsId: 'b9900d3a-ead8-44d4-bce8-ef278b9eb584', url: 'https://github.com/bisthan/maven-web-app.git'
   }

    stage('build'){
       def mavenHome = tool name: "maven_3.8.6", type: "maven"
       def mavenCMD = "${mavenHome}/bin/mvn"
       sh "${mavenCMD} clean package"
    }

    stage('code quality scan'){
        withSonarQubeEnv(credentialsId: 'sonar') {
        def mavenHome = tool name: "maven_3.8.6", type:"maven"
        def mavenCMD = "${mavenHome}/bin/mvn"
        sh "${mavenCMD} sonar:sonar"
        }
    }

    stage('upload artifact'){
        nexusArtifactUploader artifacts: [[artifactId: '01-maven-web-app', classifier: '', file: 'target/01-maven-web-app.war', type: 'war']], credentialsId: 'nexus', groupId: 'in.ashokit', nexusUrl: '35.85.33.71:8081', nexusVersion: 'nexus3', protocol: 'http', repository: 'ashokit-snapshot-repository', version: '1.0-SNAPSHOT'
    }
}