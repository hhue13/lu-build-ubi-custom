#!/usr/bin/env groovy
import se.goteborg.jenkins.LocalEnvironmentBuilder
import se.goteborg.jenkins.Pipeline

def imageBuilder = new LocalEnvironmentBuilder()

String versionFormat = '${BUILD_YEAR,XXXX}.${BUILD_WEEK,XX}_${BUILDS_THIS_WEEK,XX}'
String tagFormat = '${tag}_${version}'

try {
    node {
        timeout(time: 20, unit: 'MINUTES') {
            imageBuilder.build(versionFormat, tagFormat)
        }
    }

} catch(err) {
	new Pipeline().sendToSlack( "#jenkins", "warning", "Jenkins Failure when building docker image centos.custom in job build-ubi9-custom" )
    currentBuild.result = 'FAILURE'
}