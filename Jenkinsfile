import groovy.json.JsonSlurper
import java.time.*

node {	
	env.Release_Prefix="Test-Mono-react-repo"	
	env.AUTOBUILD="false"
	env.WORKSPACE="dev"
	List<String> sourceChanged=new ArrayList<String>()
	echo "test console"
	stage('call for build') {
		def changeLogSets = currentBuild.rawBuild.changeSets
		echo "  changeLogSets: ${changeLogSets}"				
		for (int i = 0; i < changeLogSets.size(); i++) {
			def entries = changeLogSets[i].items
			for (int j = 0; j < entries.length; j++) {
				def entry = entries[j]
				echo "${entry.commitId} by ${entry.author} on ${new Date(entry.timestamp)}: ${entry.msg}"
				def files = new ArrayList(entry.affectedFiles)
				for (int k = 0; k < files.size(); k++) {
					def file = files[k]
					String path="${file.path}"
					print path
					sourceChanged.add(path)
				}
			}
		}
		print sourceChanged.length
		echo "abcd1234"
	
	}
	stage('Git Checkout') {
        steps {
            script {
                git branch: 'main',
                    credentialsId: 'TestMonoRepoName',
                    url: 'https://github.com/praveenkumar3489/testReactMonoRepo.git'
            }
        }
    }
    stage('Build AppOne') {
        dir('./appone'){
            sh "npm install"
            sh "npm run build"
            stash includes: 'build/**', name: 'buildfiles'
            echo "build successful"
        } 
    }
}
