import groovy.json.JsonSlurper
import java.time.*

node {	
	env.Release_Prefix="Test-Mono-react-repo"	
	env.AUTOBUILD="false"

	if ("${env.AUTOBUILD}" == "true"){
		@NonCPS
		String getChangedFilesList() {
		    changedFiles = []
		    for (changeLogSet in currentBuild.changeSets) {
		        for (entry in changeLogSet.getItems()) { // for each commit in the detected changes
		            for (file in entry.getAffectedFiles()) {
		                changedFiles.add(file.getPath()) // add changed file to list
		            }
		        }
		    }
		    return changedFiles
		}
		echo "inside if"
	}else{
		echo "test console"
		@NonCPS
		String getChangedFilesList() {
		    changedFiles = []
		    for (changeLogSet in currentBuild.changeSets) {
		        for (entry in changeLogSet.getItems()) { // for each commit in the detected changes
		            for (file in entry.getAffectedFiles()) {
		                changedFiles.add(file.getPath()) // add changed file to list
		            }
		        }
		    }
		    return changedFiles
		}
		getChangedFilesList();
	}
}
