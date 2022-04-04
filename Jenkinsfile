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
checkout([$class: 'GitSCM', branches: [[name: '*/master']], extensions: [], userRemoteConfigs: [[credentialsId: 'gitcredentails', url: 'https://github.com/rohithkv16/javaparser-maven-sample.git']]])
bat 'mvn -B -DskipTests clean package'
}
}
stage('Test') {
steps {



bat 'mvn test -Dmaven.test.failure.ignore=true'
}
}
stage('sonar') {
steps {



bat 'mvn sonar:sonar -Dsonar.login=8746280db4bca8c2aabe37ebcd8f75f36843f4fe'
}
}
stage('nexus'){
    steps {
      nexusArtifactUploader artifacts: [[artifactId: 'pom.javaparser-maven-sample', classifier: '', file: 'pom.xml', type: 'pom']], credentialsId: 'nexus cr', groupId: 'pom.com.yourorganization', nexusUrl: 'localhost:8081', nexusVersion: 'nexus3', protocol: 'http', repository: 'maven4', version: 'pom.1.0-SNAPSHOT'  
    }
}
}
}