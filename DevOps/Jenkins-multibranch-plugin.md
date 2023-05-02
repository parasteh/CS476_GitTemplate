# Jenkins Multibranch Pipeline

Normally, [Jenkins pipelines][pipeline] and [Multibranch pipelines][multibranch]
requires a developer to save a `Jenkinsfile` in their repository root on one or
more branches.  The Pipeline Multibranch Defaults Plugin allows a Jenkins
administrator to specify a default `Jenkinsfile` so that developers do not need
to have a `Jenkinsfile` in their repository.

### Create a default Jenkinsfile

Before pipelines can be configured to use a default Jenkinsfile, one must
configure a groovy script in the global Config File Management provided by the
[Configfile-Provider Plugin][config-file-provider].

1. Visit _Manage Jenkins_ menu.
2. Visit _Manage files_ menu.

3. Add a new config file of type **Groovy file**.  During this step you can give
   your config file the Script ID `Jenkinsfile` or whatever ID you would like.
   Leaving it to be a UUID is fine as well.
4. Fill in the settings for the config file.

### Create a Multibranch Pipeline job

Create a new multibranch pipeline job as one normally would (or update an
existing multibranch pipeline job).  In the menu on the left, choose `New Item`
and select multibranch pipeline.

# Example default Jenkinsfile

### Default scripted pipeline

A default scripted pipeline `Jenkinsfile` which does not allow user a
repository `Jenkinsfile` to run.

```groovy
node {
    stage("Hello world") {
        echo "Hello world"
    }
}
```

A default scripted pipeline `Jenkinsfile` which loads a repository
`Jenkinsfile`.  Use case is adding required security scans or additional
auditing steps.

```groovy
node('security-scanner') {
    stage('Pre-flight security scan') {
        checkout scm
        sh '/usr/local/bin/security-scan.sh'
    }
}
try {
    node {
        stage('Prepare Jenkinsfile environment') {
            checkout scm
        }
        // now that SCM is checked out we can load and execute the repository
        // Jenksinfile
        load 'Jenkinsfile'
    }
} catch(Exception e) {
    throw e
} finally {
    stage('Post-run auditing') {
        // do some audit stuff here
    }
}
```

### Default declarative pipeline

Using [declarative pipeline][pipeline] as your default Jenkinsfile is also
possible.  Here's an example:

```groovy
pipeline {
    agent none
    stages {
        stage('Pre-flight security scan') {
            agent 'security-scanner'
            steps {
                sh '/usr/local/bin/security-scan.sh'
            }
        }
        stage('Load user Jenkinsfile') {
            agent any
            steps {
                load 'Jenkinsfile'
            }
        }
    }
    post {
        always {
            stage('Post-run auditing') {
                // do some audit stuff here
            }
        }
    }
}
```

# Example Job DSL configuration

```groovy
multibranchPipelineJob('example') {
    // SCM source or additional configuration

    factory {
        pipelineBranchDefaultsProjectFactory {
            // The ID of the default Jenkinsfile to use from the global Config
            // File Management.
            scriptId 'Jenkinsfile'

            // If enabled, the configured default Jenkinsfile will be run within
            // a Groovy sandbox.
            useSandbox true
        }
    }
}

```
[basic-branch-build-strategies]: http://wiki.jenkins.io/display/JENKINS/Basic+Branch+Build+Strategies+Plugin
[config-file-provider]: https://github.com/jenkinsci/config-file-provider-plugin
[job-dsl]: https://wiki.jenkins-ci.org/display/JENKINS/Job+DSL+Plugin
[multibranch]: https://jenkins.io/doc/book/pipeline/multibranch/
[pipeline]: https://jenkins.io/doc/book/pipeline/
[sandbox]: https://jenkins.io/doc/book/managing/script-approval/
[scm-filter-branch-pr]: https://wiki.jenkins.io/display/JENKINS/SCM+Filter+Branch+PR+Plugin
[script-console]: https://wiki.jenkins.io/display/JENKINS/Jenkins+Script+Console
[step-load]: https://jenkins.io/doc/pipeline/steps/workflow-cps/#code-load-code-evaluate-a-groovy-source-file-into-the-pipeline-script
