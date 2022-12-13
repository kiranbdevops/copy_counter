Skip to content
Search or jump to…
Pull requests
Issues
Codespaces
Marketplace
Explore
 
@kiranbdevops 
kiranbdevops
/
copy_counter
Public
Code
Issues
Pull requests
Actions
Projects
Wiki
Security
Insights
Settings
copy_counter/Jenkinsfile
@kiranbdevops
kiranbdevops Update Jenkinsfile
Latest commit 6e3cad3 25 minutes ago
 History
 1 contributor
74 lines (49 sloc)  1.65 KB

pipeline{
    
    agent any 
    
    stages {
        
        stage('Git Checkout'){
            
            steps{
                
                script{
                    
                    git branch: 'main', url: 'https://github.com/kiranbdevops/copy_counter.git'
                }
            }
        }
        stage('UNIT testing'){
            
            steps{
                
                script{
                    
                    sh 'mvn test'
                }
            }
        }
        stage('Integration testing'){
            
            steps{
                
                script{
                    
                    sh 'mvn verify -DskipUnitTests'
                }
            }
        }
        stage('Maven build'){
            
            steps{
                
                script{
                    
                    sh 'mvn clean install'
                }
            }
        }
        stage('Static code analysis'){
            
            steps{
                
                script{
                    
                    withSonarQubeEnv(credentialsId: 'sonar-api') {
                        
                        sh 'mvn clean package sonar:sonar'
                    }
                   }
                    
                }
            }
            stage('Quality Gate Status'){
                
                steps{
                    
                    script{
                        
                       waitForQualityGate abortPipeline: false, credentialsId: 'sonar-api'
                             
                    }
                }
            }
			stage('Upload file to Nexus'){
                
                steps{
                    
                    script{
                        
                    nexusArtifactUploader artifacts:
					 [
						[
							artifactId: 'springboot', 
							classifier: '', 
							file: 'target/Uber.jar', 
							type: 'jar'
							]
						], 
						
						credentialsId: 'nexus-auth', 
						groupId: 'com.example', 
						nexusUrl: '3.139.98.242:8081/', 
						nexusVersion: 'nexus3', 
						protocol: 'http', 
						repository: 'demoapp-release', 
						version: '1.0.0'   
                             
                    }
                }
            }
        }
        
}
