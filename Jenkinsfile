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
                    deploy("DEV")
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
                    deploy("STG") //, 2020)
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
                    deploy("PRD") //, 3030)
                }
            }
        }
        stage('Tests on PrePRD') {
            steps {
                script{
                    test("PRD")
                }
            }
        }
        stage('Deploy to PRD') {
            steps {
                script{
                    deploy("PRD") //, 3030)
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
    //bat "C:\\Program Files\\nodejs\\node.exe"
    //bat "C:\\Users\\richu\\AppData\\Roaming\\npm\\npm install"
    //bat "C:\\Program Files\\nodejs\\npm install"
    bat "C:\\Users\\richu\\PraktDarbs_ar_Jenkins\\npm install"
}

def deps(){
    echo "Installing pip dependencies"
    git branch: 'main', poll: false, url: 'https://github.com/mtararujs/python-greetings.git'
    bat "dir"
    bat "C:\\Python311\\Scripts\\pip install -r requirements.txt"
}

def deploy(String environment){ 
    echo "Deployment to ${environment} has started.."
    git branch: 'main', poll: false, url: 'https://github.com/mtararujs/python-greetings.git'
    bat "C:\\Users\\richu\\AppData\\Roaming\\npm\\pm2 delete \"greetings-app-${environment}\" & EXIT /B 0"
    bat "dir"
    //bat "C:\\Users\\richu\\AppData\\Roaming\\npm\\pm2 start app.py --name\"greetings-app-${environment}\""
}

def test(String environment){ 
    echo "Testing  ${environment} has started.." 
    git branch: 'main', poll: false, url: 'https://github.com/mtararujs/course-js-api-framework.git'
}

//C:\Users\richu\PraktDarbs_ar_Jenkins>