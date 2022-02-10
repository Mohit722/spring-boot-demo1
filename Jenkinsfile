pipeline{
    agent any
	stages{
        stage('Cloning repo'){
            steps{
                sh "https://github.com/Mohit722/spring-boot-demo1.git"
            }
        }
   stage('Build'){
            tools{
               maven 'M2'
            }
            steps{
                dir('spring-boot-demo1'){
                    sh "mvn clean package"
                }
            }
        }
        
             
	  stage ('Test'){
		  steps{
			  dir('spring-boot-demo1'){
				  sh "mvn clean test"
			  }
		  }
		  post {
			  always{
				 junit 'spring-boot-demo1/TestCalculator_JUnitResult.xml'

			  }
		  }
	  }
        stage('Deploy to tomcat') {
            steps {
            dir('spring-boot-demo1'){
               deploy adapters: [tomcat9(credentialsId: 'tomcat' , path: '', url: 'http://ec2-15-207-115-111.ap-south-1.compute.amazonaws.com:8080')], contextPath: null, war: 'target/sparkjava-hello-world-1.0.war'
        }
    }
    }
}
    }
