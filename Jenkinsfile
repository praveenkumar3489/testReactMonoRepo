import groovy.json.JsonSlurper
import java.time.*

node {	
	env.Release_Prefix="Test-Mono-react-repo"	
	env.AUTOBUILD="false"

	if ("${env.AUTOBUILD}" == "true"){
		when { 
	        allOf {
	            not { branch 'main' }
	            changeset "appone/**"
	            expression {  // there are changes in some-directory/...
	                sh(returnStatus: true, script: 'git diff  origin/main --name-only | grep --quiet "^appone/.*"') == 0
	            }
	            expression {   // ...and nowhere else.
	                sh(returnStatus: true, script: 'git diff origin/main --name-only | grep --quiet --invert-match "^appone/.*"') == 1
	            }
	        }
	    }
		echo "inside if"
	}else{
		echo "test console"
		when { 
	        allOf {
	            not { branch 'main' }
	            changeset "appone/**"
	            expression {  // there are changes in some-directory/...
	                sh(returnStatus: true, script: 'git diff  origin/main --name-only | grep --quiet "^appone/.*"') == 0
	            }
	            expression {   // ...and nowhere else.
	                sh(returnStatus: true, script: 'git diff origin/main --name-only | grep --quiet --invert-match "^appone/.*"') == 1
	            }
	        }
	    }
	}
}
