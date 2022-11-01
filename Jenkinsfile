pipeline{
  agent any
    
  stages{
    stage('Checkout'){
      steps{        
        git branch: 'master', credentialsId: 'github_connect', url: 'https://github.com/mhhjo123/jk_test.git'
      }
    }
    
    
    stage('Build'){
      steps{        
        bat "javac src/jenkins/Main.java"
      }
    }
    
    stage('Deploy'){
      steps{
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
    }
    
    stage('End'){
      steps{
        echo "test complete!"
      }
    }
    
  }
}
