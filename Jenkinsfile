pipeline {
    agent any
    triggers{ pollSCM('*/1 * * * *') }
    
    stages {
        stage('Build') {
            steps {
                script{
                    build()
                }
            }
        }
        stage('Install pip deps') {
            steps {
                script{
                    deps()
                }
            }
        }
        stage('Deploy to DEV') {
            steps {
                script{
                    deploy("DEV", 7001)
                }
            }
        }
        stage('Tests on DEV') {
            steps {
                script{
                    test("DEV")
                }
            }
        }
        stage('Deploy to STG') {
            steps {
                script{
                    deploy("STG", 7002) 
                }
            }
        }
        stage('Tests on STG') {
            steps {
                script{
                    test("STG")
                }
            }
        }
        stage('Deploy to PrePRD') {
            steps {
                script{
                    deploy("PrePRD", 7003) 
                }
            }
        }
        stage('Tests on PrePRD') {
            steps {
                script{
                    test("PrePRD")
                }
            }
        }
        stage('Deploy to PRD') {
            steps {
                script{
                    deploy("PRD", 7004)
                }
            }
        }
        stage('Tests on PRD') {
            steps {
                script{
                    test("PRD")
                }
            }
        }
    }
}

def build(){
    echo "Installing all required dependencies"
    powershell "C:\\Users\\richu\\AppData\\Roaming\\npm\\npm install"
}

def deps(){
    echo "Installing pip dependencies"
    git branch: 'main', poll: false, url: 'https://github.com/mtararujs/python-greetings.git'
    bat "dir"
    bat "C:\\Python311\\Scripts\\pip install -r requirements.txt"
}

def deploy(String environment, int port){ 
    echo "Deployment to ${environment} has started.."
    git branch: 'main', poll: false, url: 'https://github.com/mtararujs/python-greetings.git'
    bat "C:\\Users\\richu\\AppData\\Roaming\\npm\\pm2 delete \"greetings-app-${environment}\" & EXIT /B 0"
    powershell "C:\\Users\\richu\\AppData\\Roaming\\npm\\pm2 start app.py --name\"greetings-app-${environment}\" --${port}"
}

def test(String environment){ 
    echo "Testing  ${environment} has started.." 
    git branch: 'main', poll: false, url: 'https://github.com/mtararujs/course-js-api-framework.git'
}
