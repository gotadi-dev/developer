#!/usr/bin/env groovy
//Author: Trung Huynh
pipeline {
   agent {
       node { 
       label 'uat-srv-81'
   }
   }
       environment {
          time = func()
          def vault_profile = "prod"
          def version_img = String.format("v%s.%s", time, env.BUILD_NUMBER)
    }

stages {
    stage("[Stage] EnvApp"){
          steps {
          sh '''
        supervisorctl stop mkdocs
        rm -fr /var/www/documents
                '''
              }
            }
    stage("[Stage] Build") {   
                steps {
                    sh '''
        cp -R /var/lib/jenkins/workspace/UAT-s1-mkdocs /var/www/documents
         '''
            }
            }  

    stage("[Stage] Start") {     
                steps {
                    sh '''
        cd /var/www/documents
        pwd
        timeout 20s supervisorctl start mkdocs
         '''
            }
            }              
}
}
def func () {
   def now = new Date()
   return now.format("yyMMdd.HHmm", TimeZone.getTimeZone('UTC'))
}