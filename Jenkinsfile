//GitHub repazitorijs - https://github.com/SamantaLinda/PraktDarbs_ar_Jenkins/tree/main


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
        stage('Deploy to dev') {
            steps {
                script{
                    deploy("dev", 7001)
                }
            }
        }
        stage('Tests on dev') {
            steps {
                script{
                    test("greetings","dev")
                }
            }
        }
        stage('Deploy to staging') {
            steps {
                script{
                    deploy("staging", 7002) 
                }
            }
        }
        stage('Tests on staging') {
            steps {
                script{
                    test("greetings","staging")
                }
            }
        }
        stage('Deploy to preprod') {
            steps {
                script{
                    deploy("preprod", 7003) 
                }
            }
        }
        stage('Tests on preprod') {
            steps {
                script{
                    test("greetings","preprod")
                }
            }
        }
        stage('Deploy to prod') {
            steps {
                script{
                    deploy("prod", 7004)
                }
            }
        }
        stage('Tests on prod') {
            steps {
                script{
                    test("greetings","prod")
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
    echo "Installing pip"
    git branch: 'main', poll: false, url: 'https://github.com/mtararujs/python-greetings.git'
    bat "dir"
    bat "C:\\Python311\\Scripts\\pip install -r requirements.txt"
}

def deploy(String environment, int port){ 
    echo "Deployment to ${environment} has started.."
    git branch: 'main', poll: false, url: 'https://github.com/mtararujs/python-greetings.git'
    powershell "C:\\Users\\richu\\AppData\\Roaming\\npm\\npm install"
    bat "C:\\Users\\richu\\AppData\\Roaming\\npm\\pm2 delete \"greetings-app-${environment}\" & EXIT /B 0"
    powershell "C:\\Users\\richu\\AppData\\Roaming\\npm\\pm2 start app.py --name\"greetings-app-${environment}\" --${port}"
}

def test(String test_set, String environment){ 
    echo "Testing  ${test_set} test set on ${environment} has started.." 
    git branch: 'main', poll: false, url: 'https://github.com/mtararujs/course-js-api-framework.git'
    powershell "C:\\Users\\richu\\AppData\\Roaming\\npm\\npm install"
    powershell "C:\\Users\\richu\\AppData\\Roaming\\npm\\npm run ${test_set} ${test_set}_${environment}"
}
