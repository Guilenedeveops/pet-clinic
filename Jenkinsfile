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
        SONAQUBE_CRED = 'sonar-cred'
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
    }
}