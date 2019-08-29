pipeline{
    environment {
    def customImage = ''
  }
    
    agent any
    stages {
    stage('Git')
    {
	    steps {
    checkout scm
	    }
    }
    
    stage('Build')
    {
	    steps {
		    script {
    docker.withRegistry('https://registry.hub.docker.com', 'docker-hub') {

        customImage = docker.build("simeensheikh/DVWA1")
    }
    }
    }
	}
	    
    stage('Aqua')
	    {
		    steps
		    {
			    script {
				     aquaMicroscanner imageName: 'simeensheikh/DVWA1', notCompliesCmd: '', onDisallowed: 'ignore', outputFormat: 'html'
			    }
		    }
	    }

        stage ('PushImage')
		{
	    steps {
		    script {
			  
		 docker.withRegistry('https://registry.hub.docker.com', 'docker-hub') {    
        /* Push the container to the custom Registry */
        customImage.push()
			}
		    }
			}
			}
    }
}
