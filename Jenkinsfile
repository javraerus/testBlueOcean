import hudson.FilePath
timestamps {
    node ('master') {
        stage ('Build Polyspace results') {
            echo "hello2"
        }
        
        /*
        step([$class: 'WarningsPublisher',
consoleParsers: [
[parserName: 'Java Compiler (javac)'],
],
canComputeNew: true,
canResolveRelativePaths: true,
canRunOnFailed: true,
categoriesPattern: '',
defaultEncoding: '',
excludePattern: '',
healthy: '1000',
includePattern: '',
messagesPattern: '',
unHealthy: '100000'])
        */
        stage('Scan for Polyspace warnings-8') {
            step([
                $class: 'WarningsPublisher',
                parserConfigurations: [[
                    parserName: 'LK_BugFinder_Defects_Parser',
                    pattern: 'prueba.xml'
                ]
            ]])
        }
        stage('Publish HTML reports') {
            publishHTML([
                allowMissing:          false,
                alwaysLinkToLastBuild: true,
                keepAll:               true,
                reportDir:             'Variant/RdW/Target/Release/Polyspace/BugFinder/_result/_result/html/',
                reportFiles:           'link2metricserver.html',
                reportName:            'Project on Polyspace Metric Server'])
        }

    }
}
