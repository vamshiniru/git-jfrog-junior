pipeline {
  agent {label 'master'}
      tools { 
        maven 'maven' 
        jdk 'java8' 
    }
    
    stages {
        stage('git clone') {
            steps {
                echo 'cloning git repo'
                git 'http://ec2-54-82-12-211.compute-1.amazonaws.com/root/mytestrepo.git'
            }
        }
    
        stage('Build') {
            steps {
                echo 'Building..'
                sh 'mvn clean'
                sh 'mvn install'
                }  
             }
        stage('Test') {
            steps {
                echo 'Testing..'
                echo 'all test cases passed'
          }
        }
        
        stage('Deploy Artifacts') { 
             steps {
                script {			 
                     def server = Artifactory.server 'jfro' 
                     def uploadSpec = """{
                       "files": [
                            {
                              "pattern": "/var/lib/jenkins/workspace/MyTestJob/target/*.war",
                              "target": "myrepo/"
                            }
                                ]
                    }"""
	                server.upload(uploadSpec)
	            }
	          }
	        }
	        
	       }
	       }