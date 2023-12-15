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
    }
}
