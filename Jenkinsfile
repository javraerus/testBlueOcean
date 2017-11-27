import hudson.FilePath
timestamps {
    node ('master') {
        stage ('Build Polyspace results') {
            echo "hello"
        }
        stage('Scan for Polyspace warnings') {
            step([
                $class: 'WarningsPublisher',
                parserConfigurations: [[
                    parserName: 'LK_BugFinder_Defects_Parser',
                    pattern: 'prueba.txt'
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
