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
}

def deps(){
    echo "Installing all required dependencies"
}

def deploy(String environment){ 
    echo "Deployment to ${environment} has started.."
}

def test(String environment){ 
    echo "Testing ${test_set} test set on ${environment} has started.." 
}