node {

    def app



   stage('clone repo'){
    checkout scm
   }


   stage('build image'){


        sh """
        #!/bin/bash

        docker login  -u admin -p admin mycluster.icp:8500
        docker build -t mycluster.icp:8500/ace/aceappzoli .
        docker push mycluster.icp:8500/ace/aceappzoli



        """
   }


}