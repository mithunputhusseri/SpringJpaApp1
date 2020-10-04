def myVariable = "pipeline"
pipeline {

  agent any

  stages {	


	stage('Maven Compile'){

		steps{
script{
                        myVariable = "Maven Compile"
			echo 'Project compile stage'

			sh 'mvn compile'

	       	}
}

	}

	stage('Unit Test') {

	   steps {
script{
                        myVariable = "Unit Test"

			echo 'Project Testing stage'

	       

       		}
}

   	}

	  
	stage('Jacoco Coverage Report') {

        steps{
script{
                        myVariable = "Jacoco Coverage Report"

            jacoco()

		}
}
	}

	  

	stage('SonarQube analysis') {
		steps{
script{
                        myVariable = "SonarQube report analysis"
    withSonarQubeEnv('SonarQube2') {
      sh 'mvn sonar:sonar'
	 
    } 
}
	
  }
}
	  
stage("Quality Gate") {
            steps {
script{
                        myVariable = "Quality Gate"
                timeout(time: 1, unit: 'HOURS') {
          
                    waitForQualityGate abortPipeline:true
                }
            }
}
        }
	stage('Run JMeter Test')
	  {
		  steps{
script{
                        myVariable = "Jmeter Run Test"
		//cd C:\\apache-jmeter-5.3\\bin
	  	//bat label: 'JMeter', script: 'C:\\apache-jmeter-5.3\\bin\\jmeter -Jjmeter.save.saveservice.output_format=xml -n -t C:\\Users\\mitp\\Desktop\\tmp\\results.jmx -l C:\\Users\\mitp\\Desktop\\tmp\\Test.jtl'
		  sh 'sudo /home/ec2-user/jmeter/apache-jmeter-5.3/bin/./jmeter.sh -n -t /home/ec2-user/jmeter/apache-jmeter-5.3/bin/examples/files/results.jmx -l /home/ec2-user/jmeter/apache-jmeter-5.3/bin/examples/files/Test.jtl'
		  }  
}
	}
	stage('Maven Package'){

		steps{
script{
                        myVariable = "Maven Package"

			echo 'Project packaging stage'


		}
}
	} 


	

    

  }
post {
        success {
            mail to: 'mithunputhusseri@gmail.com',
             subject: "Succeded Pipeline: ${currentBuild.fullDisplayName}",
             body: "Build is successfully completed"
        }
	     failure {
        mail to: 'mithunputhusseri@gmail.com',
             subject: "Failed Pipeline: ${currentBuild.fullDisplayName}",
             body: "Something is wrong with ${env.BUILD_URL} and failed to pass through ${myVariable} stage"
    }
    }

}
