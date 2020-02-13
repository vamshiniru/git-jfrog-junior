pipeline {
  agent {label 'master'}
      tools { 
        maven 'maven' 
        jdk 'java' 
    }
    
    stages {
        stage('git clone') {
            steps {
                echo 'cloning git repo'
                git 'http://13.230.194.203/root/my_first_project1.git'
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
                     def server = Artifactory.server 'My_task' 
                     def uploadSpec = """{
                       "files": [
                            {
                              "pattern": " /var/lib/jenkins/workspace/file1_master/target/mvn-hello-world.war",
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