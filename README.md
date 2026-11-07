srk
.github/workflows/build-apk.yml
name: Build SRK Media Player APK

on:
  push:
    branches: [ "main", "master" ]
  workflow_dispatch:

jobs:
  build:
    runs-on: ubuntu-latest

    steps:
      - name: Checkout repository code
        uses: actions/checkout@v4

      - name: Set up JDK 17
        uses: actions/setup-java@v4
        with:
          java-version: '17'
          distribution: 'temurin'

      - name: Setup Gradle
        uses: gradle/actions/setup-gradle@v3
        with:
          gradle-version: '8.7'

      - name: Build Debug APK
        run: |
          if [ -f "./gradlew" ]; then
            chmod +x ./gradlew
            ./gradlew assembleDebug --stacktrace
          else
            gradle assembleDebug --stacktrace
          fi

      - name: Upload Compiled APK
        uses: actions/upload-artifact@v4
        with:
          name: SRK-Media-Player-Ready-APK
          path: app/build/outputs/apk/debug/*.apk
          
