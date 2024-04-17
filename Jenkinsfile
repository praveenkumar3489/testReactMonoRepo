import groovy.json.JsonSlurper
import java.time.*

node {	
	env.Release_Prefix="Test-Mono-react-repo"	
	env.AUTOBUILD="false"
	env.WORKSPACE="dev"
	List<String> sourceChanged=new ArrayList<String>()
	echo "test console"
	agent any
	agent {
        docker {
            image 'node:6-alpine'
            args '-p 3000:3000'
        }
    }
    environment {
        CI = 'true' 
    }
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
		git(
	       url: 'https://github.com/praveenkumar3489/testReactMonoRepo.git',
	       credentialsId: '756c599f-4414-447b-a627-fd9c811765a8',
	       branch: "main"
	    )
        // step {
            // script {
            //     git branch: 'main',
            //         credentialsId: '756c599f-4414-447b-a627-fd9c811765a8',
            //         url: 'git@github.com/praveenkumar3489/testReactMonoRepo.git'
            // }
            echo "git checkout complete"
        // }
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
