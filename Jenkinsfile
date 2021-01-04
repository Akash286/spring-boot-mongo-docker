node
{
    def mavenHome = tool name: "maven"
    def buildNumber = BUILD_NUMBER
    
   environment
    {
         PATH = "$PATH:/usr/bin/docker-compose"
    }
    stage('checkout code from github')
    {
        git credentialsId: '8ad2f092-8f52-455d-baff-5759b8e05bf3', url: 'https://github.com/Akash286/spring-boot-mongo-docker.git'
    }
    stage('creating packages with maven')
    {
        sh "${mavenHome}/bin/mvn clean package"
    }
    stage('creating images with docker')
    {
        sh "docker build -t dockerakashde/spring-boot-mongo:${buildNumber} ."
    }
   /* stage('docker login and push')
    {
       withCredentials([string(credentialsId: 'dockerhubpwd', variable: 'dockerhubpwd')]) {
    // some block
    sh "docker login -u dockerakashde -p ${dockerhubpwd}"
}
    sh "docker push  dockerakashde/spring-boot-mongo:${buildNumber}"
        
    }*/
    stage('running App in remote server')
    {
       // sshagent(['024b57d3-84f3-431e-8b49-faaea1760c6f']) {
    // some block
    sh "docker-compose -f docker-compose.yml up -d"
// }
    }
}
