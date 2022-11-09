pipeline {
    agent anytools {
    maven 'maven-3.8.6' 
  }
  environment{
    PATH = "/opt/maven3/bin:$PATH"
  }
    stages {
        stage('checkoutScm'){
          checkout([
        $class: 'GitSCM', 
        branches: [[name: '*/master2']], 
        doGenerateSubmoduleConfigurations: false, 
        extensions: [[$class: 'CleanCheckout']], 
        submoduleCfg: [], 
        userRemoteConfigs: [[credentialsId: '<gitCredentials>', url: 'https://github.com/rama100000/myrepo.git']]
    ])
        }

        stage('Build') {
            steps {
                sh 'mvn -f hello-app/pom.xml -B -DskipTests clean package'
            }
            post {
                success {
                    echo "Now Archiving the Artifacts....."
                    archiveArtifacts artifacts: '**/*.jar'
                }
            }
        }
        stage('Test') {
            steps {
                sh 'mvn -f hello-app/pom.xml test'
            }
            post {
                always {
                    junit 'hello-app/target/surefire-reports/*.xml'
                }
            }
        }
    }
}
