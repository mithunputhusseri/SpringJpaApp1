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

	       

       		}

   	}

	  
	stage('Jacoco Coverage Report') {

        steps{

            jacoco()

		}

	}

	  

	stage('SonarQube analysis') {
		steps{
    withSonarQubeEnv('SonarQube') {
      bat label: '', script: '''mvn clean package sonar:sonar \
		 -Dsonar.host.url=http://3.238.72.11:9000 \
 		-Dsonar.login=03659a70455e6013aa2417d0013af6aff7cde0de'''
    } 
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
		//cd C:\\apache-jmeter-5.3\\bin
	  	bat label: 'JMeter', script: 'C:\\apache-jmeter-5.3\\bin\\jmeter -Jjmeter.save.saveservice.output_format=xml -n -t C:\\Users\\mitp\\Desktop\\tmp\\results.jmx -l C:\\Users\\mitp\\Desktop\\tmp\\Test.jtl'
		  }  
	}

    

  }
	post {
        always {
            emailext body: 'A Test EMail', recipientProviders: [[$class: 'DevelopersRecipientProvider'], [$class: 'RequesterRecipientProvider']], subject: 'Test'
        }
    }

}
