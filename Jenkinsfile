pipeline {
    agent any

    triggers
    {
        //Query repository every minute
        pollSCM('* * * * *')
    }

    stages {

        // Step 1: Performs the below activities
        //                  1. Archive the config file from repo where changes occured
        //                  2. Push the archive in nexus
      
        stage('Archive parameters') {
            steps {
                    
                    sh """
                        env=( Dev Qa Ci)
                        for envName in "${env[@]}"
                        do
                         for servicename in $(find $envName/ -maxdepth 1 -mindepth 1 -type d);
                          do
                            echo $servicename
                            #rm -f "${servicename}.zip"
                          done
                        done 
                      """ 
                    
                  /*  zip (
                      archive: true, 
                      dir: 'Dev/assessment-service', 
                      glob: '', 
                      zipFile: 'Dev/assessment-service.zip'
                      ) */
            }
        }


        stage('> Push the archive in nexus') {
            steps {
                   
                   echo "Push archive to nexus"
 /*                    nexusArtifactUploader (
                      artifacts: [
                          [
                            artifactId: 'assessment-service', 
                            classifier: '', 
                            file: 'Dev/assessment-service.zip', 
                            type: 'zip'
                          ]
                       ], 
                       credentialsId: 'nexus3_vm', 
                       groupId: 'com.ebrd.Dev', 
                       nexusUrl: '10.199.44.21:8081', 
                       nexusVersion: 'nexus3', 
                       protocol: 'http', 
                       repository: 'ebrd_external_app_config', 
                       version: '1.0.0')  */
            }
        }

   }
}
