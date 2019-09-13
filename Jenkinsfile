pipeline {
    agent any
    tools {
        maven 'maven'
    }
    options {
//        skipDefaultCheckout(true)
        parallelsAlwaysFailFast()
    }
    stages {
//        stage('Checkout') {
//            steps {
//                git 'https://github.com/Mitschi/simpleservice.git'
//            }
//        }
        stage('Build') {
            steps {
                sh 'mvn -DskipTests=true clean package'
            }
        }
        stage('Test') {
            steps {
                sh 'mvn clean test'
            }
        }
        parallel {
            stage('Acceptance Testing') {
                stages {
                    stage('Deploy to Acceptance Testing Env') {
                        echo 'Deploy Acceptance Testing'
                    }
                    stage('Acceptance Testing') {
                        echo 'Acceptance Testing'
                    }
                }
            }
            stage('Performance Testing') {
                stages {
                    stage('Deploy to Performance Testing Env') {
                        echo 'Deploy Performance Testing'
                    }
                    stage('Performance Testing') {
                        echo 'Performance Testing'
                    }
                }
            }
        }
        stage('Results') {
            steps {
                junit '**/target/surefire-reports/TEST-*.xml'
                archiveArtifacts 'target/*.jar'
            }
        }
    }
}

//    stages {
//        stage('Preparation') { // for display purposes
//            // Get some code from a GitHub repository
//            git 'https://github.com/Mitschi/simpleservice.git'
//            // Get the Maven tool.
//            // ** NOTE: This 'M3' Maven tool must be configured
//            // **       in the global configuration.
//            mvnHome = tool 'maven'
//        }
//        stage('Build') {
//            // Run the maven build
//            withEnv(["MVN_HOME=$mvnHome"]) {
//                if (isUnix()) {
//                    sh '"$MVN_HOME/bin/mvn" clean package'
//                } else {
//                    bat(/"%MVN_HOME%\bin\mvn" clean package/)
//                }
//            }
//        }
//        stage("Unit Testing") {
//            echo 'Unit Testing'
//        }
//
//failFast true
//        parallel {
//            stage('Acceptance Testing') {
//                stages {
//                    stage('Deploy to Acceptance Testing Env') {
//                        echo 'Deploy Acceptance Testing'
//                    }
//                    stage('Acceptance Testing') {
//                        echo 'Acceptance Testing'
//                    }
//                }
//            }
//            stage('Performance Testing') {
//                stages {
//                    stage('Deploy to Performance Testing Env') {
//                        echo 'Deploy Performance Testing'
//                    }
//                    stage('Performance Testing') {
//                        echo 'Performance Testing'
//                    }
//                }
//            }
//        }
//
//        stage('Results') {
//            junit '**/target/surefire-reports/TEST-*.xml'
//            archiveArtifacts 'target/*.jar'
//        }
//    }