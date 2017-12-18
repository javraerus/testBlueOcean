pipeline {

  // agent defines where the pipeline will run.
  agent {
    // This also could have been 'agent any' - that has the same meaning.
    label ""
    // Other possible built-in agent types are 'agent none', for not running the
    // top-level on any agent (which results in you needing to specify agents on
    // each stage and do explicit checkouts of scm in those stages), 'docker',
    // and 'dockerfile'.
  }
  
  // The tools directive allows you to automatically install tools configured in
  // Jenkins - note that it doesn't work inside Docker containers currently.
 

  stages {
    // At least one stage is required.
    stage("first stage") {
      // Every stage must have a steps block containing at least one step.
      steps {
        // You can use steps that take another block of steps as an argument,
        // like this.
        //
        // But wait! Another validation issue! Two, actually! I didn't use the
        // right type for "time" and had a typo in "unit".
        timeout(time: true, uint: 'MINUTES') {
          echo "We're not doing anything particularly special here."
          echo "Just making sure that we don't take longer than five minutes"
          echo "Which, I guess, is kind of silly."
          
          // This'll output 3.3.3, since that's the Maven version we
          // configured above. Well, once we fix the validation error!
          sh "mvn -version" 
        }
      }
      
      // Post can be used both on individual stages and for the entire build.
    }
    
    stage('second stage') {
      // You can override tools, environment and agent on each stage if you want.

      
      steps {
        echo "This time, the Maven version should be 3.3.9"
    checkpoint 'Completed tests'

      }
    }
    
    stage('third stage') {
      steps {
        // Note that parallel can only be used as the only step for a stage.
        // Also, if you want to have your parallel branches run on different
        // nodes, you'll need control that manually with "node('some-label') {"
        // blocks inside the parallel branches, and per-stage post won't be able
        // to see anything from the parallel workspaces.
        // This'll be improved by https://issues.jenkins-ci.org/browse/JENKINS-41334, 
        // which adds Declarative-specific syntax for parallel stage execution.
        sh kjhkjhkjh
      }
  }
  
  


}

}
