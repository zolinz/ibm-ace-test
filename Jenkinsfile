node {

    def app

  env.DOCKER_API_VERSION="1.23"

   stage('clone repo'){
    checkout scm
   }


   stage('build image'){


        sh """
        #!/bin/bash

        docker build -t zoliapp .
        """
   }


}