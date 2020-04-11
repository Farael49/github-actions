# github-actions
An example of a maven based project using github actions 

Github offers premade workflows that we can choose on the website 
Either on the project "actions" tab or by browsing the available starters on https://github.com/actions/starter-workflows/tree/master/ci 

Quite similar to a Jenkinsfile/Travis/.. pipeline's description, we setup the different steps we want to run with the following

    - name: Step to run
      run: cmd to run

We can have multiple workflows, and configure a few things : 

https://help.github.com/en/actions/reference/workflow-syntax-for-github-actions

When to trigger the build :

    - on:
        push:
          branches: [ master, test]
        pull_request:
          branches: [ feature/* ]

Which environment to target (a custom runner can also be provided):

    - jobs:
        build:
          runs-on: ubuntu-latest

Java oriented : 

Setting up a specific JDK version (currently defaults to JDK8/x64) :

    - name: Set up JDK 1.14
      uses: actions/setup-java@v1
      with:
        java-version: 1.14
        architecture: x64

Getting a JDK from a specific provider :

    - run: curl -O https://download.java.net/java/early_access/jdk15/18/GPL/openjdk-15-ea+18_linux-x64_bin.tar.gz
    - name: Set up JDK 15
      uses: actions/setup-java@v1
      with:
        java-version: 15
        jdkFile: openjdk-15-ea+18_linux-x64_bin.tar.gz

Caching Maven dependencies :

    - name: Cache Maven packages
      uses: actions/cache@v1
      with:
        path: ~/.m2
        key: ${{ runner.os }}-m2-${{ hashFiles('**/pom.xml') }}
        restore-keys: ${{ runner.os }}-m2
        
Uploading your Jar (or any generated artifact) to github :

      - uses: actions/checkout@v2
      - uses: actions/setup-java@v1
      - run: mvn -B package --file pom.xml
      - run: mkdir staging && cp target/*.jar staging
      - uses: actions/upload-artifact@v1
        with:
          name: Package
          path: staging
