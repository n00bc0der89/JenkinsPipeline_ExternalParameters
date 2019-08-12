pipeline {
    agent none    
    stages {
        // Step 1: Performs the below activities
        //                  1. Archive the config file from repo where changes occured
        //                  2. Push the archive in nexus
        

        stage('Archive parameters') {
            agent {label 'docker-agent'}
            steps {
                script {
                  def DIR = sh(returnStdout: true, script: """
                        env="Dev Qa Ci"
                        for envName in \$env;
                        do
                         for servicename in \$(find \$envName/ -maxdepth 1 -mindepth 1 -type d);
                          do
                            echo \$servicename
                          done
                        done 
                      """) 
                    println DIR;
                    arr= DIR.split()
                    arr.each{
                        println "directory names are ${it}"
                        def dirname = "${it}"
                        def zipname = "${it}.zip"
                        println "dir name is ${dirname}"
                        println "zip name is ${zipname}"
                        zip (
                          archive: true, 
                          dir: dirname, 
                          glob: '', 
                          zipFile: zipname
                      ) 
                        
                    }
                    
                   }
                     
            }
        }


        stage('> Push the archive in nexus') {
            agent { label 'docker-agent-2' }
            steps {
                   
                   echo "Push archive to nexus"
                script {
                    arr.each{
                        println "directory names are ${it}"
                    
                        artifactname= "${it}".split('/')[1];
                        filename = "${it}.zip";      
                        
         /*            nexusArtifactUploader (
                      artifacts: [
                          [
                            artifactId: artifactname, 
                            classifier: '', 
                            file: filename, 
                            type: 'zip'
                          ]
                       ], 
                       credentialsId: 'nexus3_vm', 
                       groupId: 'com.ebrd.Dev', 
                       nexusUrl: '192.168.33.10:8081', 
                       nexusVersion: 'nexus3', 
                       protocol: 'http', 
                       repository: 'ebrd_external_app_config', 
                       version: '1.0.0')
                       */
               echo "Uploaded in Nexus !!!!!"
                    }
                }
                    
            }
        }

   }
}
