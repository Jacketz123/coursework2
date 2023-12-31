pipeline
{
    agent any
            
    environment
    {
        DOCKER_IMAGE_NAME='jacketz123/coursework2:latest'
    }
    
    stages
    {
        stage('Build Docker Image')
        {
            steps
            {
                script
                {
                    docker.build(DOCKER_IMAGE_NAME, '-f Dockerfile .')
                }
            }
        }         
        stage('Test Docker Image')
        {
            steps
            {
                script
                {
                    docker.image(DOCKER_IMAGE_NAME).inside
                    {
                        sh 'echo "Container Launched Successfully"'
                    }
                }
            }
        }       
        stage('Push Image to DockerHub')
        {
            steps
            {
                script
                {
                    withCredentials([string(credentialsId: 'dockerhub-pwd', variable: 'dockerhubpwd')]) {
                    sh 'docker login -u jacketz123 -p ${dockerhubpwd}'
}
                    sh 'docker push jacketz123/coursework2:latest'
                }
            }
        }
        stage('Deploy to Kubernetes')
        {
            steps
            {
                sshagent(['Production_Key'])
                {
                    sh "ssh -t -t ubuntu@ip-172-31-55-121 -o StrictHostKeyChecking=no \'kubectl set image deployment/coursework2 coursework2=jacketz123/coursework2:latest'"
                }
            }
        }
    }
}
