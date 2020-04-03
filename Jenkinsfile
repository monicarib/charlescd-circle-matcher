// This Source Code Form is subject to the terms of the Mozilla Public
// License, v. 2.0. If a copy of the MPL was not distributed with this
// file, You can obtain one at https://mozilla.org/MPL/2.0/.

@Library('ZupSharedLibs@darwin') _

node {
    try {

        buildDockerBuilder {
            dockerRepositoryName = "darwin-circle-matcher"
            dockerBuilderImage = "adoptopenjdk/openjdk11:jdk-11.0.4_11-alpine-slim"
            dockerFileBuilder = "DockerfileBuilder"
            dockerFileLocation = "."
            team = "Realwave"
        }

        mvnBuildWithCompose {
            composeFileName = "docker-compose-ci.yml"
            composeService = "darwin-circle-matcher"
            composeProjectName = "darwin-circle-matcher"
            team = "Realwave"
            useBuilder="true"
        }

        stage('SonarQube analysis') {
            def scannerHome = tool 'Sonar Zup';
            withSonarQubeEnv('Sonar Zup') {
                sh "${scannerHome}/bin/sonar-scanner"
            }
        }

        buildDockerContainer {
            dockerRepositoryName = "darwin-circle-matcher"
            dockerFileLocation = "."
            team = "Realwave"
        }

    } catch (e) {
        notifyBuildStatus {
            buildStatus = "FAILED"
        }
        throw e
    }

}