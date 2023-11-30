pipeline {
    agent { label "dev-server"}
    stages {
        
        stage("code stage"){
            steps{
                git url: "https://github.com/KaranThakur99/node-todo-cicd.git", branch: "master"
                echo 'code stage pr hai'
            }
        
        }
        stage("build and test"){
            steps{
                sh "docker build -t node-app-test-new:latest ." 
                echo 'code build hogya hai'
                
            }
        }
        stage("scan image"){
            steps{
                echo "image scanning hogyi"
                
            }
        }
        stage("push to dockerhub"){
            steps{ 
                withCredentials([usernamePassword(credentialsId:"dockerHub",passwordVariable:"DOCKERHUBPass",usernameVariable:"DOCKERHUBUser")]){
                sh "docker login -u ${env.DOCKERHUBUser} -p ${env.DOCKERHUBPass}"
                sh "docker tag node-app-test-new:latest ${env.DOCKERHUBUser}/node-app-test-new:latest"
                sh "docker push ${env.DOCKERHUBUser}/node-app-test-new:latest"
                echo 'code ko push krdiya hai'
                }
            }
        }
        stage("deploy"){
            steps{
                sh 'docker-compose down && docker-compose up -d'
                echo 'deploy b krdenge'
                
            }
            
        }
    
    }
}
