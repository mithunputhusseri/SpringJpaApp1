pipeline {

  agent any

  stages {	


	stage('Maven Compile'){

		steps{

			echo 'Project compile stage'

			bat label: 'Compilation running', script: '''mvn compile'''

	       	}

	}

	stage('Unit Test') {

	   steps {

			echo 'Project Testing stage'

			bat label: 'Test running', script: '''mvn test'''

	       

       		}

   	}

	  
	stage('Jacoco Coverage Report') {

        steps{

            jacoco()

		}

	}

	  

	stage('SonarQube'){

         steps{

            bat label: '', script: '''mvn sonar:sonar \

		 -Dsonar.host.url=http://localhost:9000 \

 		-Dsonar.login=ff5c276939ab066fea300810e7006165c6243c7b'''

          }

      }

	  

	stage('Maven Package'){

		steps{

			echo 'Project packaging stage'

			bat label: 'Project packaging', script: '''mvn package'''

		}

	} 
	stage('Run JMeter Test')
	  {
		  steps{
			bat label: 'Moving to folder', script: 'cd C:\\Program Files\\apache-jmeter-5.3\\bin'  
	  	bat label: 'JMeter', script: 'jmeter -Jjmeter.save.saveservice.output_format=xml -n -t C:\\Users\\mitp\\Desktop\\tmp\\results.jmx -l C:\\Users\\mitp\\Desktop\\tmp\\Test.jtl'
		  }  
	}

    

  }
	post {
        always {
            emailext body: 'A Test EMail', recipientProviders: [[$class: 'DevelopersRecipientProvider'], [$class: 'RequesterRecipientProvider']], subject: 'Test'
        }
    }

}
