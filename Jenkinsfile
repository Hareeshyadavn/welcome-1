
pipeline {
    
    agent {label 'slave'}
    
    environment {
        IMAGE_TAG = "${BUILD_NUMBER}"
    }
    
    
        stage('Build Docker'){
            steps{
                script{
                    sh '''
                    echo 'Build Docker Image'
                    cd python-jenkins-argocd-k8s/
                    docker build -t yadavn1692/repositry1:v2 . 
                    '''
                }
            }
        }

        stage('Push the artifacts'){
           steps{
                script{
                    sh '''
                    echo 'Push to Repo'
                    docker push yadavn1692/repositry1:v2
                    '''
                }
            }
        }
        
       
        
        stage('Update K8S manifest & push to Repo'){
            steps {
                script{
                   
                        sh '''
                        cd /python-jenkins-argocd-k8s/deploy/
                        cat deploy.yaml
                        sed -i '' "s/v2/v3/g" deploy.yaml
                        cat deploy.yaml
                        git add deploy.yaml
                        git commit -m 'Updated the deploy yaml | Jenkins Pipeline'
                        git remote -v
                        git push 
                        '''                        
                    
                }
            }
        }
    }
}
