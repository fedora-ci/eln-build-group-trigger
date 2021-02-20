#!groovy

properties(
    [
        parameters(
            [
                string(description: 'CI Message', defaultValue: '', name: 'CI_MESSAGE'),
            ]
        ),
	
        pipelineTriggers(
            [
		[
		    $class: 'CIBuildTrigger',
		    noSquash: true,
		    providerData: [
                        $class: 'RabbitMQSubscriberProviderData',
                        name: 'RabbitMQ',
			
                        overrides: [
                            topic: 'org.fedoraproject.prod.bodhi.update.status.testing.koji-build-group.build.complete',
                            queue: 'osci-pipelines-queue-13'
                        ],

			checks: [
                            [
                                expectedValue: '^f35$',
                                field: '$.artifact.release'
                            ]
			]
                    ]
                ]
	    ]
        )
    ]
)

def msg

pipeline {

    agent any

    stages {
        stage('Print') {
            steps {
                script {
                    msg = readJSON text: CI_MESSAGE
		    println msg  
                }
            }
        }
    }
}
