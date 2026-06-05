@Library("Shared_library") _
pipeline{
    agent {label 'linux'}
    
    stages{
        // helloe World!
        stage("Start"){
            steps{
                script{
                    my_first_Groovy()
                }
            }
        }
        stage("Code"){
            steps{
                script{
                    cloneCode("https://github.com/chirayu-webkorps/django-notes-app/","main")
                }
            }
        }
        stage("Build"){
            steps{
                script{
                    Build_Docker('notes-app', 'latest', 'chirayu-webkorps' );
                }
            }
        }
        stage("Push to DockerHub"){
            steps{
                script{
                    DokcerHub_Push("notes-app", "latest")
                }
            }
        }
        stage("Deploy"){
            steps{
                echo "Deploying..."
                sh '''
                docker rm -f notes-app || true
                
                docker run -d \
                --name notes-app \
                --env-file /home/jenkins/workspace/DjangoCICD/.env \
                -p 8000:8000 \
                notes-app:latest 
                '''
            }
        }
    }
}
