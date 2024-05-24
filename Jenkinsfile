pipeline{
    agent any 
    tools{
        maven 'maven'
    }
        stages{
            stage('Build'){
                steps{
                    sh '''
                    mvn clean package -DskipTests
                    '''             
                }        
            }
            stage('Test'){
                steps{
                    sh 'mvn test'
                }
            }
            stage('Sonar'){
                environment{
                    scanner = tool 'SONAR_SCANER'
                }
                steps{
                    withSonarQubeEnv('SONAR'){
                        sh "${scanner}/bin/sonar-scanner -e -Dsonar.host.url=http://172.17.0.1:9000 -Dsonar.projectKey=Backend -Dsonar.java.binaries=target -Dsonar.exclusions=src/test/**"
                    }
                }

            } 
        pipeline{
            agent any 
                Stages{
                    Stage('Stage 1'){
                        steps{
                            echo             
                    }        
                }    
            }
        }
        stage('QualityGate'){
                    steps {
                        sleep(10)
                        timeout(1){
                            withForQualityGate abortPipeline:false, credentialsId: 'token_sonar'
                                }
                         }
                        }   


               
        }
    }
