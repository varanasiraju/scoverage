pipeline {
   agent any
    stages { 
        stage('compile-package'){
        sh "${sbtHome} package"
    }
    
    stage('scoverage'){
        sh "${sbtHome} clean coverage test"
    }
    
   stage('scoverage-report'){
        sh "${sbtHome} coverageReport"
    
    step([$class: 'ScoveragePublisher', reportDir: 'target/scala-2.12/scoverage-report', reportFile: 'scoverage.xml'])   
    }
    
 stage('Scala JUnit Test'){
        junit 'target/test-reports/*.xml'
    }
  }
}
