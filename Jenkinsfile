pipeline {
  agent any
  tools {
    maven 'maven3.8.6' 
  }
  stages {
    stage ('checkout code') {
      steps {
        checkout scm([$class: 'GitSCM',
                        branches: [[name: '*/main']],
                        doGenerateSubmoduleConfigurations: false,
                        extensions: [[$class: 'CleanCheckout']],
                        submoduleCfg: [],
                        userRemoteConfigs: [[credentialsId: 'git-credentials', url: ' https://github.com/rama100000/myrepo.git']]
                    ])

        }
      }
    }
   stage ('Build') {
      steps{
        sh 'mvn clean package'
    } 

  }
   
  }
}
