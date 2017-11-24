timestamps {
    node ('debejenk007') {
        
        def checkoutTools = new CheckoutTools()
        
        stage ('checkout Appl'){
            checkoutTools.checkoutAll(Checkout.buildCheckout2(env, SVN_URL, [
                ['Source',                       './Source',                       'infinity', true, 'UpdateWithCleanUpdater'],
                ['Tools/Make',                   './Tools/Make',                   'infinity', true, 'UpdateWithCleanUpdater'],
                ['Tools/Polyspace',              './Tools/Polyspace',              'infinity', true, 'UpdateWithCleanUpdater'],
            ]))
        }

        stage ('Build Polyspace results') {
            bat '''\
                @echo off
                @set CI_SERVER=ON
                @rem @set ECLIPSE_HOME=%CI_ECLIPSE_MS14_4_INTERIM%
                @set ECLIPSE_HOME=%CI_ECLIPSE_MS16_2%
                @set MINGW=%ECLIPSE_HOME%/mingw/bin
                @rem @set MSYS=%ECLIPSE_HOME%/msys/bin
                @set MSYS=%ECLIPSE_HOME%/msys64/usr/bin
                @set PATH=%PATH%;%MSYS%;%ECLIPSE_HOME%
                @set CI_CCV850=%CI_GHS_517D%
                @set CI_POLY_PATH=%CI_R2017B%
                @set PS_BUILD_ID=%BUILD_ID%
                
                @rem setting manually the name of the Polyspace Test Release
                @rem # this ReleaseName will be the recognition name on the servers, so make sure you see your variant and branch here i.e. to make the assignment for everybody one-to-one
                @set ReleaseName=P07580_MEB_OCC_PS_BF_TRUNK
                echo ReleaseName=%ReleaseName%
                
                @set WORKSPACE_JS='%WORKSPACE%'
                @set PS_PROGNAME_LAST_BUILT_TEMP='${JENKINS_SHARE}/ps_prog_name_timestamp_lastbuilt_temp.txt'
                
                echo Build ID of jenkins Job %PS_BUILD_ID%
                rmdir /S /Q ".\\JenkinsServerStack" >nul 2>&1 || echo.
                ::xcopy "\\de141607.de.kostal.int\\JenkinsServerStack\\%ReleaseName%\\*" ".\\JenkinsServerStack\"  /Y /C >nul 2>&1 || echo.
                xcopy "\\de141607.de.kostal.int\\JenkinsServerStack\\%ReleaseName%\\*" "Variant/RdW/Target/Release/Polyspace/BugFinder/_result/"  /Y /C >nul 2>&1 || echo.
                cd Tools\\Make
                
                @rem # Start Makefile with correct target for Polyspace Bugfinder Complete Run # 
                echo Start Polyspace Bugfinder Complete Run.
                ::call make.bat RdW Release "NONE" -j16 run_complete_polyspace_bf

            '''.stripIndent()
            archive 'Variant/RdW/Target/Release/Polyspace/BugFinder/_result/**/*'
        }
        stage('Scan for Polyspace warnings') {
            step([
                $class: 'WarningsPublisher',
                parserConfigurations: [[
                    parserName: 'LK_BugFinder_Defects_Parser',
                    pattern: 'Variant/RdW/Target/Release/Polyspace/BugFinder/_result/Polyspace-Doc/ResultsBL_List_annotationfilter.txt'
                ]
            ]])
            step([
                $class: 'WarningsPublisher',
                parserConfigurations: [[
                    parserName: 'LK_Polyspace',
                    pattern: 'Variant/RdW/Target/Release/Polyspace/BugFinder/_result/Polyspace-Doc/ResultsBL_List_annotationfilter.txt'
                ]
            ]])
            
            step([
                $class: 'WarningsPublisher',
                parserConfigurations: [[
                    parserName: 'LK_Polyspace_Bf',
                    pattern: 'Variant/RdW/Target/Release/Polyspace/BugFinder/_result/Polyspace-Doc/ResultsBL_List_annotationfilter.txt'
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
