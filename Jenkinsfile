pipeline {
   agent any
    stages { 
        stage('compile-package') {
           steps {
              def sbtHome = tool name: 'sbt', type: 'org.jvnet.hudson.plugins.SbtPluginBuilder$SbtInstallation'
              sh "${sbtHome}/bin/sbt compile"

             }
        }
    }
}
    
    
