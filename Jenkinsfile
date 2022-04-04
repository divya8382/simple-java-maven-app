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
stage('sonar')
steps {
bat 'mvn sonar:sonar -Dsonar.login=db0fd46aa08a00880658a95fc3cbdb4ae2c7ab4f'
}
}
}
}
