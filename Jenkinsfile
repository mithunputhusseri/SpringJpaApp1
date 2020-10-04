pipeline {

  agent any

  stages {	


	stage('Maven Compile'){

		steps{

			echo 'Project compile stage'

			sh 'mvn compile'

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
    withSonarQubeEnv('SonarQube2') {
      sh 'mvn sonar:sonar'
	 
    } 
	
  }
}
	  
stage("Quality Gate") {
            steps {
                timeout(time: 1, unit: 'HOURS') {
          
                    waitForQualityGate abortPipeline:true
                }
            }
        }
	stage('Run JMeter Test')
	  {
		  steps{
		//cd C:\\apache-jmeter-5.3\\bin
	  	bat label: 'JMeter', script: 'C:\\apache-jmeter-5.3\\bin\\jmeter -Jjmeter.save.saveservice.output_format=xml -n -t C:\\Users\\mitp\\Desktop\\tmp\\results.jmx -l C:\\Users\\mitp\\Desktop\\tmp\\Test.jtl'
		  }  
	}
	stage('Maven Package'){

		steps{

			echo 'Project packaging stage'


		}

	} 
	

    

  }

}
