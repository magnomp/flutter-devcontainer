# flutter-devcontainer

Dev Containers leverage docker containers to provide you with a standardized environment to work on a given project. In this case we have a sample dev container configuration which provides a development machine with JVM/Android SDK/Flutter SDK already set up

Provided you have Docker installed and the Dev Containers extension on your VS Code, just open this project and you`ll be prompted to switch to the dev container environment. Confirm it and that`s all.

To use it on you real project, just copy the .devcontainer folder to the project root. Maybe you`ll have to edit the Dockerfile in order to match your project specifics requirements on flutter version, jdk version, etc

Based on https://github.com/lucashilles/flutter-dev-container