node {

    imageName = "mycluster.icp:8500/ace/aceappzoli7"



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


   stage('test helm install'){
    sh"""
    #!/bin/bash

   #kubectl create serviceaccount --namespace kube-system tiller
   #kubectl create clusterrolebinding tiller-cluster-rule --clusterrole=cluster-admin --serviceaccount=kube-system:tiller
   #kubectl patch deploy --namespace kube-system tiller-deploy -p '{"spec":{"template":{"spec":{"serviceAccount":"tiller"}}}}'

   #sysctl -w net.ipv6.conf.all.disable_ipv6=1

    
   helm init --client-only --debug
   #helm version --tls
   helm list --tls



    """
   }


   stage('deploy new image'){

        sh """
        docker login  -u admin -p admin mycluster.icp:8500
       kubectl get image aceappzoli7 -n=ace -o yaml | sed 's/scope: namespace/scope: global/g' | kubectl replace -f -
         kubectl set image deployment/zoli-ace-01-ibm-ace zoli-ace-01-ibm-ace=${imageName}


         kubectl rollout status deployment/zoli-ace-01-ibm-ace

        """

   }


}