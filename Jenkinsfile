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
    }
}
