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
        SONAQUBE_INSTALLATION = 'sonar'
        SONAQUBE_CRED = '1a84cfa7-f013-4177-ba3a-2c7aa4b48d82'
        SCANNER_HOME = tool 'sonar-env'
        APP_NAME = 'guigui'
    }
    stages{
        stage('Git Checkout'){
            steps{
                git branch: "${BRANCH_NAME}", credentialsId: "${GIT_CRED}", \
                url: "${PROJECT_URL}"
            }
        }
        stage('Trivy Scan'){
            steps{
                 sh "trivy fs --format table -o maven_dependency.html ."
            }
        }
        stage('Unit Test'){
            steps{
                sh 'mvn clean'
                sh 'mvn compile -DskipTest'
                
            }
        }
        stage('Sonarqube Scan'){
            steps{
                withSonarQubeEnv(credentialsId: "${SONAQUBE_CRED}", \
                installationName: "${SONAQUBE_INSTALLATION}" ) {
              sh ''' $SCANNER_HOME/bin/sonar-scanner -Dsonar.projectName=${APP_NAME} -Dsonar.projectKey=${APP_NAME} \
                   -Dsonar.java.binaries=. '''
}
            }

        }
        stage('Quality Gate Check'){
            steps{
              script{
                 waitForQualityGate abortPipeline: false, credentialsId: "${SONAQUBE_CRED}" 
              }
            }
        }
        stage('Code Package'){
            steps{
                sh 'mvn package'
            }
        }
        stage('Upload Jar to Jfrog'){
            steps{
                withCredentials([usernamePassword(credentialsId: "${JFROG_CRED}", \
                 usernameVariable: 'ARTIFACTORY_USER', passwordVariable: 'ARTIFACTORY_PASSWORD')]) {
                    script {
                        // Define the artifact path and target location
                        //def artifactPath = 'targe
    }
    }
}
}
    }
    }