pipeline{
    agent any
    tools{
        jdk 'java11'
        terraform 'Terraform'
    }
    environment {
        SCANNER_HOME=tool 'sonar-scanner'
    }
    stages {
        stage('clean workspace'){
            steps{
                cleanWs()
            }
        }
        stage('git checkout'){
            steps{
                git branch: 'main', url: 'https://github.com/pradyumna93/Project-1.git'
            }
        }
        stage ('terraform version'){
            steps{
                sh 'terraform --version'
            }
        }
        stage('sonar analysis'){
            steps{
                withSonarQubeEnv('sonar-server'){
                    sh'''$$SCANNER_HOME/bin/sonar-scanner\
                    -Dsonar.projectName=jenkins \
                    -Dsonar.projectKey=jenkins '''
                }
            }
        }
        stage("quality gate"){
           steps {
                script {
                    waitForQualityGate abortPipeline: false, credentialsId: 'Sonar-token' 
                }
            } 
        }
    }
}
