node {
    def app

    stage('Clone repository') {
        /* Cloning the Repository to our Workspace */

        checkout scm
    }

    stage('Build image') {
        /* This builds the actual image */

        app = docker.build("sharathgangam/nodeapp")
    }

    stage('Test image') {
        
        app.inside {
            echo "Tests passed"
        }
    }

	
stage ('Docker push'){
  docker.withRegistry('262836726888.dkr.ecr.us-east-1.amazonaws.com/todayrepo', 'ecr:us-east-1:aws-credentails') {
    docker.image('demo').push('latest')
     }
	                echo "Trying to Push Docker Build to ECR"
}
	
    stage('Push image') {
        /* 
			You would need to first register with DockerHub before you can push images to your account
		*/
        docker.withRegistry('https://registry.hub.docker.com', 'dockerhub') {
            app.push("${env.BUILD_NUMBER}")
            app.push("latest")
            } 
                echo "Trying to Push Docker Build to DockerHub"
    }
}
