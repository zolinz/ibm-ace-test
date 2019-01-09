node {

    imageName = "mycluster.icp:8500/ace/aceappzoli2"



   stage('clone repo'){
    checkout scm
   }


   stage('build image and push to ICP registry'){


        sh """
        #!/bin/bash

        docker login  -u admin -p admin mycluster.icp:8500
        docker build -t ${imageName} .
        docker push ${imageName}
        """
   }


   stage('deploy new image'){

        sh """
         kubectl set image deployment/zoli-ace-01-ibm-ace zoli-ace-01-ibm-ace=${imageName}


         kubectl rollout status deployment/zoli-ace-01-ibm-ace

        """

   }


}