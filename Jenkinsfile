pipeline { 
    agent any 
    stages { 
        stage('Clean Workspace') { 
            steps { cleanWs() } 
        } 
        stage('Code Checkout') { 
            steps { 
                git branch: 'main', url: 'https://github.com/Sharmila127/Calculator
app.git' 
            } 
        } 
        stage('Docker Build') { 
            steps { 
                script { 
                    sh 'docker image prune -f' 
                    sh 'docker rmi -f myapp:latest || true' 
                    docker.build("myapp:latest") 
                } 
            } 
        } 
        stage('Deploy') { 
            steps { 
                script { 
                    sh ''' 
                    if [ "$(docker ps -q -f name=mycalcapp-container)" ]; then 
                        docker stop mycalcapp-container 
                    fi 
                    if [ "$(docker ps -a -q -f name=mycalcapp-container)" ]; then 
                        docker rm mycalcapp-container 
                    fi 
                    docker run -d --name mycalcapp-container -p 5000:5000 
myapp:latest 
                    ''' 
                } 
            } 
        } 
    } 
}
