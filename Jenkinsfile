node {
    checkout([$class: 'GitSCM', 
				branches: [[name: "origin/master"]], 
				userRemoteConfigs: [[
                url: 'https://github.com/dandu1008/scripted-when-changeset.git']],
				])
	def changesetFound = false
	def changeLogSets = currentBuild.changeSets
	println "changeLogSets: ${changeLogSets}"
	println "changeLogSets.size(): ${changeLogSets.size()}"
	
	for (i = 0; i < changeLogSets.size(); i++) {
	    println changeLogSets[i].getClass().getName()
	    
	    def entries = changeLogSets[i].items
	    println "${entries}"
	    for (j = 0; j < entries.length; j++) {
	        def entry = entries[j]
	        println "${entry}"
	        //println "${entry.msg}"
	        def files = new ArrayList(entry.affectedFiles)
	        for (k = 0; k < files.size(); k++) {
	            def file = files[k]
	            println "changed file: ${file.path}"
	            if (file.path.startsWith("set/") && file.path.endsWith(".js") && !file.path.startsWith("set/test/")) {
	                println "matched file: ${file.path}"
	                changesetFound = true
	            }
	        }
	    }
	    
	    if (changesetFound)
	       break
	}
	
	changeLogSets = null // have to set it to null otherwise it would throw the searialization error.
	echo "ChangesetFound: ${changesetFound}"
	
	if (changesetFound) {
	    stage('changesetFound') {
	        echo 'Changeset is found'
	    }
	}
	else {
	    stage('changesetNotFound') {
	        echo 'Changeset is not found'
	    }
	}
}
