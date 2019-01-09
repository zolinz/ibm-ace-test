node {

    imageName = "mycluster.icp:8500/ace/aceappzoli6"



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
        docker login  -u admin -p admin mycluster.icp:8500
       kubectl get image aceappzoli6 -n=ace -o yaml | sed 's/scope: namespace/scope: global/g' | kubectl replace -f -
         kubectl set image deployment/zoli-ace-01-ibm-ace zoli-ace-01-ibm-ace=${imageName}


         kubectl rollout status deployment/zoli-ace-01-ibm-ace

        """

   }


}