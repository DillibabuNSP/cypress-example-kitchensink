pipeline {
    agent {
        docker {
            label 'default'
            image 'cypress/base:14.16.0'
        
        }
    }
    stages {
        stage('Install Dependencies') { 
            steps {
                echo "Running build ${env.BUILD_ID} on ${env.JENKINS_URL}"
                sh 'npm ci'
                sh 'npm run cy:verify'
            }
        }
        
        stage('CBS UI Test') { 
            environment {
                CYPRESS_RECORD_KEY = credentials('cypress-record-key')
                CYPRESS_trashAssetsBeforeRuns = 'false'
            }

            parallel {
                stage('Tester A') {
                    steps {
                        echo "Running build ${env.BUILD_ID} on Tester A"
                        sh "NO_COLOR=1 xvfb-run -a npx cypress-cloud run --parallel --record --key ${env.CYPRESS_RECORD_KEY}"
                    }
                }

                stage('Tester B') {
                    steps {
                        echo "Running build ${env.BUILD_ID} on Tester B"
                       sh "NO_COLOR=1 xvfb-run -a npx cypress-cloud run --parallel --record --key ${env.CYPRESS_RECORD_KEY}"
                    }
                }

                stage('Tester C') {
                    steps {
                        echo "Running build ${env.BUILD_ID} on Tester C"
                       sh "NO_COLOR=1 xvfb-run -a npx cypress-cloud run --parallel --record --key ${env.CYPRESS_RECORD_KEY}"
                    }
                }

            }
           
        }
    }
}
