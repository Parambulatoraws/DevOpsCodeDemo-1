
        pipeline{
            tools{
                jdk 'myjava'
                maven 'mymaven'
            }
            agent none
            stages{
                stage('Checkout on master'){
                    agent any
                    steps{
                echo 'cloning...'
                        git 'https://github.com/RayItern/DevOpsCodeDemo-1.git'
                    }
                }
                stage('Compile on slave1'){
                    agent {label 'slave1'}
                    steps{
                        echo 'compiling...'
                        sh 'mvn compile'
                }
                }
                stage('CodeReview on slave2'){
                    agent {label 'slave2'}
                    steps{
                    
                echo 'codeReview...'
                        sh 'mvn pmd:pmd'
                    }
                }
                stage('UnitTest on slave1'){
                    agent {label 'slave1'}
                    steps{
                    echo 'Testing'
                        sh 'mvn test'
                    }
                    post {
                    success {
                        junit 'target/surefire-reports/*.xml'
                    }
                }	
                }
                stage('Package on master'){
                    agent any
                    steps{
                        sh 'mvn package'
                    }
                }
            }
        }
