pipeline{
    agent any 
    stages{
        stage("Code"){
            steps{
                echo "cloning the code"
                git url: "https://github.com/manishgupta577/test.git",branch:"main"
            }
        }
        stage("Build"){
            steps{
                echo "building the docker image"
                sh "docker build -t test ."
            }
        }
        stage("Push to docker hub"){
            steps{
                echo "pushing the docker image to docker hub"
                withCredentials([usernamePassword(credentialsId:"DockerHub",passwordVariable:"dockerHubPass",usernameVariable:"dockerHubUser")]){
                sh "docker tag test ${env.dockerHubUser}/test:latest" 
                sh "docker login -u ${env.dockerHubUser} -p ${env.dockerHubPass}"
                sh "docker push ${env.dockerHubUser}/demo:test"
                }
            }
        }
        stage("Deploy"){
            steps{
                echo "depolying the conatiner"
                sh "docker run -d -p 8000:8000 manish577/test:latest"
            }
        }
    }    
    
}
