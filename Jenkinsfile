pipeline{
    agent any
    tools{
        maven 'M2_HOME'
        jdk 'JAVA_HOME'
    }
    environment{
        AWS_REGION = 'us-east-1'
        GIT_CRED = 'Github-creds'
        PROJECT_URL = 'https://github.com/Guilenedeveops/pet-clinic-java-code.git'
        BRANCH_NAME = 'main'
    }
    stages{
        stage('Git Checkout'){
            steps{
                git branch: "${BRANCH_NAME}", credentialsId: "${GIT_CRED}", \
                url: "${PROJECT_URL}"
            }
        }
    }
}