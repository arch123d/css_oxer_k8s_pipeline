
# jenkins process

insllation of jenkins

yum install git,docker

kubernetes installation

aws cli installation

create credentials in jenkins for dockerhub- manage jenkins-cred-global-username-add credential- id should be match to the pipeline id
aws cred add

this is docker build stage-sh 'docker build -t ${DOCKERHUB_REPO}:${BUILD_NUMBER} oxer-html/.'

environment pass through the docker hub-{DOCKERHUB_REPO} ,collecting & found build number ${BUILD_NUMBER}

kubectl use for deploy-
stage('Deploy to Kubernetes') {
            environment {
                AWS_CREDENTIALS = 'aws_credentials'
            }
            steps {
                withCredentials([[$class: 'AmazonWebServicesCredentialsBinding', credentialsId: AWS_CREDENTIALS]]) {
                    script {
                        sh """
                    aws eks update-kubeconfig --name cluster --region ap-south-1 --kubeconfig /tmp/config # /root/.kube/config kubernets CREd store in the tmp
                    kubectl apply -f oxer-html/oxer.yml --kubeconfig=/tmp/config 
                    kubectl set image deployment/my-oxer container-oxer=${DOCKERHUB_REPO}:${env.BUILD_NUMBER} --kubeconfig=/tmp/config 
                    """


