pipeline{
    agent{ label 'dev-agent' }
    stages{
        stage('Code'){
            steps{
                git url: 'https://github.com/sowmya-bm/node-todo-cicd.git', branch: 'master'
            }
        }
        stage('Build and Test'){
            steps{
                sh 'docker build . -t sowmyabm/node-todo-app-cicd:latest'
            }
        }
          stage('Login and push image'){
            steps{
                withCredentials([usernamePassword(credentialsId:'dockerhub',passwordVariable:'dockerHubPassword',usernameVariable:'dockerHubUser')]){
                    sh "docker login -u ${env.dockerHubUser} -p ${env.dockerHubPassword}"
                    sh "docker push sowmyabm/node-todo-app-cicd:latest"
                }
            }
        }
        stage('Deploy'){
            steps{
                sh 'docker-compose down && docker-compose up -d'
            }
        }
    }
}
