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
        // stage('Tests on DEV') {
        //     steps {
        //         script{
        //             test( "greetings", "DEV")
        //         }
        //     }
        // }
        // stage('Deploy to STG') {
        //     steps {
        //         script{
        //             deploy("STG") //, 2020)
        //         }
        //     }
        // }
        // stage('Tests on STG') {
        //     steps {
        //         script{
        //             test("STG")
        //         }
        //     }
        // }
        // stage('Deploy to PRD') {
        //     steps {
        //         script{
        //             deploy("PRD") //, 3030)
        //         }
        //     }
        // }
        // stage('Tests on PRD') {
        //     steps {
        //         script{
        //             test("PRD")
        //         }
        //     }
        // }
    }
}

def build(){
    echo "Building of node application is starting.."
    git branch: 'main', poll: false, url: 'https://github.com/mtararujs/course-js-api-framework.git'
    bat "npm install"
}

def deps(){
    echo "Installing all required dependencies"
    bat "npm install"
    //git branch: 'main', poll: false, url: 'https://github.com/mtararujs/python-greetings.git'
   // bat "npm install -g pm2"
    bat "dir"
    //bat "pip3 install -r requirements.txt"
   // bat "npm install --save-dev mocha"
    //bat "npm test"
}

def deploy(String environment){ 
    echo "Deployment to ${environment} has started.."
    //git branch: 'main', poll: false, url: 'https://github.com/mtararujs/python-greetings.git'
    bat "dir"
    //bat "C:\\Users\\Samanta\\AppData\\Roaming\\npm\\pm2 delete \"greetings-app-${environment}\" & EXIT /B 0"
    //bat "C:\\Users\\Samanta\\AppData\\Roaming\\npm\\pm2 start app.py --name \"greetings-app-${environment}\" -- ${port}"
}

// def test(String test_set, String environment){ 
//     echo "Testing ${test_set} test set on ${environment} has started.." 
//     git branch: 'main', poll: false, url: 'https://github.com/mtararujs/course-js-api-framework.git'
//     bat "npm run ${test_set} ${test_set}_${environment}"
// }