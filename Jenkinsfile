node {

    def app

  env.DOCKER_API_VERSION="1.23"

   stage('clone repo'){
    checkout scm
   }


   stage('build image'){


        sh """
        #!/bin/bash

        docker login mycluster.icp:8500 -u admin -p admin
        docker build -t zoliapp .
        """
   }


}