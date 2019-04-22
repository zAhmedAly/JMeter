pipeline {
  agent {label 'AAServer01_Slave01'}
  stages {
    stage('Clone Test Script') {
      steps {
        git 'https://github.com/zAhmedAly/JMeter'
      }
    }      
    stage('Get Java Home') {
      steps {
        sh 'DT=`date +"%m-%d-%y-T%H%M%S"`'
        sh 'echo $JAVA_HOME'
        sh 'DT=`date +"%m-%d-%y-T%H%M%S"`'
      }
    }
    stage('Execute Test') {
      steps {
        sh 'DT=`date +"%m-%d-%y-T%H%M%S"`'
        sh '/apps/jmeter/bin/jmeter.sh -n -t /home/jenkins/workspace/JMeter_Pipeline/UserLoadDistribution.jmx -l /apps/jmeter/reports/jtl/TEST_${BUILD_NUMBER}.jtl -e -o /apps/jmeter/reports/Test_${BUILD_NUMBER} -Jjmeter.save.saveservice.output_format=xml -Jjmeter.save.saveservice.output_format=csv'
        sh 'DT=`date +"%m-%d-%y-T%H%M%S"`'
      }
    }
  }
post {
   success {
      sh 'mv /apps/jmeter/reports/Test_${BUILD_NUMBER} /var/www/html/reports'
     mail body: 'Load Test Results ${BUILD_NUMBER}: http://165.227.24.75/reports/Test_${BUILD_NUMBER}', from: 'Jenkins', subject: 'Load Test Results ${BUILD_NUMBER}', to: 'aaoflaca@gmail.com'
   }
}
}
