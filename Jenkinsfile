pipeline {
    agent {
  label 'Master'
}
    stages {
        stage('Checkout Github Repo') {
            steps {
            git branch: 'main', credentialsId: '10', url: 'https://github.com/Jayparmar98/dotnet.git'
            sh "ls -lah"
            }
        }

        stage('Build') {
            steps{
        sh """
        dotnet build -c Release /p:Version=${BUILD_ID}
        dotnet publish -c Release --no-build
        """
            }
        }

        stage('Nexus_Arti_Upload') {
        steps {
         sh 'zip “aspdotnet_${BUILD_TIMESTAMP}.zip”, /var/lib/jenkins/workspace/AspDotnet/asp.net/bin/Release/net6.0/publish'
         nexusArtifactUploader artifacts: [[artifactId: "Maven", classifier: "${BUILD_TIMESTAMP}", file: "aspdotnet_${BUILD_ID}.zip", type: 'zip']], credentialsId: 'NEXUS', groupId: 'Java', nexusUrl: '20.197.19.232:8081', nexusVersion: 'nexus3', protocol: 'http', repository: 'Maven-Host', version: '1.1'
       }
     }


/*         stage('Zip Folder') {
            steps {
        script {
            // Directory path to the folder you want to zip
            def sourceDir = '/var/lib/jenkins/workspace/AspDotnet/asp.net/bin/Release/net6.0/publish/'

            // Directory path where you want to create the zip file
            def targetDir = '/var/lib/jenkins/workspace/AspDotnet/asp.net/bin/Release/net6.0/publish/final_arti'

            // Name of the zip file
            def zipFileName = "aspdotnet_${BUILD_ID}.zip"

            // Command to create the zip file
            sh "cd $sourceDir && zip -r $targetDir/$zipFileName ./*"

            // Optional: Print the contents  the target directory after zipping
            sh "ls -l $targetDir"
            
        }
    }
}

         stage('Upload to Nexus') {
            steps {
        script {
            // Directory path to the artifacts you want to upload
            def artifactsDir = '/var/lib/jenkins/workspace/AspDotnet/asp.net/bin/Release/net6.0/publish/final_arti/'

            // Nexus repository URL
            def nexusUrl = 'http://20.197.19.232:8081/repository/Maven-Host/Java/Maven'

            // Nexus repository username and password for authentication
            def nexusUsername = 'admin'
            def nexusPassword = 'Jay@123'

            // Loop through the artifacts directory and upload each file to Nexus
            sh "cd $artifactsDir && find . -type f -print0 | xargs -0 -I {} curl -u $nexusUsername:$nexusPassword --upload-file {} $nexusUrl/{}"

            // Optional: Print a message after uploading all artifacts
            echo "All artifacts uploaded to Nexus successfully!"
        }
    }
}

stage('Play Ansible Playbook') {
    steps {
        script {
            // Directory path where your Ansible playbook is located
            def playbookDir = '/etc/ansible/'

            // Inventory file path
            def inventoryFile = '/etc/ansible/hosts'

            // Additional arguments to pass to the ansible-playbook command
            def extraArgs = '-e "var1=value1 var2=value2"'

            // Command to run the Ansible playbook
            sh "ansible-playbook -i $inventoryFile $extraArgs $playbookDir/jenkins.yml"
        }
    }
}
*/
        
       // stage('Zip Folder') {
         //   steps {
           //     sh "zip aspdotnet_${BUILD_ID}.zip /var/lib/jenkins/workspace/AspDotnet/asp.net/bin/Release/net6.0/publish/"
            //}
        //}

       // stage('Nexus_Arti_Upload')
    // {
     //nexusArtifactUploader artifacts: [[artifactId: "Maven", classifier: "${BUILD_TIMESTAMP}", file: "aspdotnet_${BUILD_ID}.zip", type: 'zip']], credentialsId: 'NEXUS', groupId: 'Java', nexusUrl: '20.197.19.232:8081', nexusVersion: 'nexus3', protocol: 'http', repository: 'Maven-Host', version:  '1.7'
     //}


    }
}
