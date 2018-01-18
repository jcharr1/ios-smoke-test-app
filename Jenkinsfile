#!groovy

pipeline {
	agent any

	stages 
	{
        stage('Run Calabash Tests')
        {
        	steps
       		{
                ansiColor('xterm') {
                    dir ("CalSmokeApp") {
                    	sh "hostname"
                        sh "export LANG=en_US.UTF-8"
                        sh "export LANGUAGE=en_US.UTF-8"
                        sh "export LC_ALL=en_US.UTF-8"

                        sh "bundle"
                        sh "make app-cal"
                        sh "bundle exec cucumber --name Alerts --format json --out 'cucumber/test-results.json' --color"
						step($class: 'CucumberTestResultArchiver', testResults: 'cucumber/test-results.json')
						livingDocs(featuresDir:'cucumber')
						cucumberSlackSend channel: '#il101-ios', json: 'cucumber/test-results.json'

						
                    } // dir
                } // ansiColor
            } // submit steps
        } // submit stage
    } // stages
 } // pipeline