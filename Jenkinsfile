pipeline {
  agent any
  stages {
    stage('Compile') {
      steps {
        cmake(installation: 'InSearchPath', arguments: './')
        sh '''make
cd googlemock/gtest
'''
      }
    }
    stage('Test') {
      steps {
        sh '''pwd
cd googlemock/gtest

./sample1_unittest --gtest_output=xml:sample1.xml
./sample2_unittest --gtest_output=xml:sample2.xml
./sample3_unittest --gtest_output=xml:sample3.xml
./sample4_unittest --gtest_output=xml:sample4.xml
./sample5_unittest --gtest_output=xml:sample5.xml
./sample6_unittest --gtest_output=xml:sample6.xml
./sample7_unittest --gtest_output=xml:sample7.xml
'''
      }
    }
	post {
		always {
			script {
				// Ç»Ç∫Ç©ó·äOÇ™î≠ê∂Ç∑ÇÈÇÃÇ≈try-catchÇ∑ÇÈ
				try {
					step(xunit(
						thresholds: [ skipped(failureThreshold: '0'), failed(failureThreshold: '0') ],
						tools: [ GoogleTest(pattern: 'googlemock/gtest/*.xml') ]))
				} catch(error) {
					echo ' exception'
				} finally {
					echo 'xunit end'
				}
			}
		}
	}
}