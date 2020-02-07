pipeline {
   agent any
    stages { 
        stage('Compile Source Code'){
            def sbtHome = tool name: 'sbt', type: 'org.jvnet.hudson.plugins.SbtPluginBuilder$SbtInstallation'
            sh "${sbtHome}/bin/sbt compile"
        }
    
        stage('Coverage Test'){
           def sbtHome = tool name: 'sbt', type: 'org.jvnet.hudson.plugins.SbtPluginBuilder$SbtInstallation'
            sh "${sbtHome}/bin/sbt clean coverage test"
        }
        
         stage('Package'){
           def sbtHome = tool name: 'sbt', type: 'org.jvnet.hudson.plugins.SbtPluginBuilder$SbtInstallation'
            sh "${sbtHome}/bin/sbt package"
        }
    
         stage('Coverage Report'){
            def sbtHome = tool name: 'sbt', type: 'org.jvnet.hudson.plugins.SbtPluginBuilder$SbtInstallation'
            sh "${sbtHome}/bin/sbt coverageReport"
        
         step([$class: 'ScoveragePublisher', reportDir: 'target/scala-2.12/scoverage-report', reportFile: 'scoverage.xml'])   
        } 
    
        stage('Scala JUnit Test'){
            junit 'target/test-reports/*.xml'
        }
    
        stage('Style Checks Report'){
            def sbtHome = tool name: 'sbt', type: 'org.jvnet.hudson.plugins.SbtPluginBuilder$SbtInstallation'
            sh label: '', script: 'rm -f /home/varanaka/workspace/EAP_DevOps_Project_Build_Pipeline/scalastyle-config.xml'
            sh "${sbtHome}/bin/sbt scalastyleGenerateConfig"
            sh "${sbtHome}/bin/sbt scalastyle"
            
            checkstyle canComputeNew: false, defaultEncoding: '', healthy: '', pattern: 'target/scalastyle-result.xml', unHealthy: ''
        }
     }
  }
