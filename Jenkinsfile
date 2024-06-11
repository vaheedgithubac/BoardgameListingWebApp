pipeline {
  agent none
  stages {
      
  /*  stage('Git checkout') {
      agent any
      steps {
       git branch: 'main', url: 'https://' 
      }
    }
      
   */ 
      
    stage('Gitleaks scan') {
      agent any
      steps {
       
       catchError(buildResult: 'UNSTABLE', message: 'ERROR', stageResult: 'FAILURE') {
                sh 'docker run -v /var/lib/jenkins/workspace/Gitleaks:/path -w /path zricethezav/gitleaks:latest detect --source . --verbose -f json -r gitleaks.json'
             }
      } 
    }
    
    stage('Uploading Scan results to Defect DOJO') {
        agent any
        steps {
         sh '''   python3 --version
                  python3 upload-reports.py
            '''
        }
    }



    
  }
}
