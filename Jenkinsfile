pipeline {
    agent any

    stages {
        stage ('Compile Stage') {

            steps {
                withMaven(maven : 'maven_3_5_0') {
                    sh 'mvn clean install'
                }
            }
        }

        stage ('Testing Stage') {

            steps {
                withMaven(maven : 'maven_3_5_0') {
                    sh 'mvn test-compile test'
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
                                                                           "pattern": "target/*.jar",
                                                                           "target": "generic-local/devops_pipline"
                                                                         }
                                                                            ]
                                                                }"""
	  		      
	  			                              server.upload(uploadSpec)
					         echo 'artifact uploaded'
	  			      }
      
                                       }
                               }
    }
}
