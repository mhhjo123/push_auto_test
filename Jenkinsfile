node{    
    stage("Checkout"){
        echo "Github Checkout"
        git branch: 'master', credentialsId: 'github_connect', url: 'https://github.com/mhhjo123/Jenkins_test.git'
    }          
    
    stage("Build"){        
        echo "Java Compile"
        bat "javac -target 1.8 src/jenkins/Main.java"
    }
    
    stage("Deploy"){
        echo "Deploy to Linux Server"
        sshPublisher(
            publishers: 
            [sshPublisherDesc(
                configName: 'Linux for Jenkins Test', 
                transfers: 
                [sshTransfer(
                    cleanRemote: false, 
                    excludes: '', 
                    execCommand: '''echo cd jenkins_test/src > /root/jenkins_test/jenkins_result.txt
                                    cd jenkins_test/src >> /root/jenkins_test/jenkins_result.txt
                                    echo Main.class execute >> /root/jenkins_test/jenkins_result.txt
                                    java jenkins.Main >> /root/jenkins_test/jenkins_result.txt''', 
                    execTimeout: 120000, 
                    flatten: false, 
                    makeEmptyDirs: false, 
                    noDefaultExcludes: false, 
                    patternSeparator: '[, ]+', 
                    remoteDirectory: '', 
                    remoteDirectorySDF: false, 
                    removePrefix: '', 
                    sourceFiles: 'src/jenkins/*.class')], 
                    usePromotionTimestamp: false, 
                    useWorkspaceInPromotion: false, 
                    verbose: true
            )
            ]
        )
    }
    
    stage("Test"){
        echo "Good to See you!"
    }
}
