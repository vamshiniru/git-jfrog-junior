pipeline {
  agent {label 'master'}
      tools { 
        maven 'maven' 
        jdk 'jdk' 
    }
    
    stages {
        stage('git clone') {
            steps {
                echo 'cloning git repo'
                git ' http://ec2-13-230-194-203.ap-northeast-1.compute.amazonaws.com/root/my_first_project1.git'
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