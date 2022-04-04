pipeline {
agent any
tools{
maven "maven3"
} 
stages {
stage('Hello') {
steps {
echo 'Hello World'
}
}
stage('Build') {
steps {
checkout([$class: 'GitSCM', branches: [[name: '*/master']], extensions: [], userRemoteConfigs: [[credentialsId: 'githubcredentials', url: 'https://github.com/divya8382/simple-java-maven-app.git']]])
}
}
stage('Test') {
steps {
bat 'mvn test -Dmaven.test.failure.ignore=true'
}
}
stage('sonar') {
steps {
bat 'mvn sonar:sonar -Dsonar.login=db0fd46aa08a00880658a95fc3cbdb4ae2c7ab4f'
}
}
stage('nexus') {
steps {
    nexusArtifactUploader artifacts: [[artifactId: 'pom.my-app', classifier: '', file: 'pom.xml', type: 'pom']], credentialsId: 'NEXUS_CRED', groupId: 'pom.com.mycompany.app', nexusUrl: 'localhost:8081', nexusVersion: 'nexus3', protocol: 'http', repository: 'maven-central-repository', version: 'pom.1.0-SNAPSHOT'
}
}
}
}

