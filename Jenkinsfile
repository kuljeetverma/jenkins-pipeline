pipeline {
    agent any

    stages {
        stage ('Compile Stage') {

            steps {
                withMaven(maven : 'maven_3_5_0') {
                    sh 'mvn clean compile'
                }
            }
        }

        stage ('Testing Stage') {

            steps {
                withMaven(maven : 'maven_3_5_0') {
                    sh 'mvn test'
                }
            }
        }

/*
        stage ('Deployment Stage') {
            steps {
                withMaven(maven : 'maven_3_5_0') {
                    sh 'mvn deploy'
                }
            }
        }
        */
        stage('upload on Artifactory')    {
                                 steps {
                                        echo 'Artifactory server upload'
      				      script 
	 			      {
      
                                            def server = Artifactory.server('Artifactory-server')              
                                            def uploadSpec = """{
                                                                   "files": [
      					                               {
                                                                           "pattern": "target/*.war",
                                                                           "target": "generic-local/"
                                                                         }
                                                                            ]
                                                                }"""
	  		      
	  			                              server.upload(uploadSpec)
	  			      }
      
                                       }
                               }
    }
}
