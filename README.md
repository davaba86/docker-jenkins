# Docker Jenkins

## TLDR

Updated Jenkins as Code based on Docker image `jenkins/jenkins:lts`.

## General Overview

This example used the base image and then constructs a desired image which will be used in the docker-compose setup.

The amount of plugins are kept to a minimal to ensure basic user authentication and security setup.

On top of that the config is also kept to a minimal allowing you to build your own instead of being served too many entries.

I suggest you configure the jenkins in the web-UI and then view the code so that you later can compare the yaml output with before and after.

The password is generated and saved into a local file which is then transfered into the container at `/run/secrets/adminpw`.

## Setup

The password below is just an example and I strongly recommend you to generate one of your own instead.

```bash
echo "sACZ7RGTQ_K79ML9cVjNCz4q3" > adminpw.txt
docker-compose up -d
```

> Run `docker-compose build` if you make any changes to plugins.txt as it won't be automatically detected by `docker-compose up`.

## Cleanup

```bash
docker-compose down --volumes --remove-orphans
rm adminpw.txt
```

## View Jenkins YAML Settings

Go to Manage **Jenkins -> Configuration as Code** and click on View Confiruation.

## List Installed Plugins

Enter [http://JENKINS_URL/script](http://JENKINS_URL/script) and enter the following into the console.

```bash
Jenkins.instance.pluginManager.plugins.each{
  plugin ->
    println ("${plugin.getDisplayName()} (${plugin.getShortName()}): ${plugin.getVersion()}")
}
```

## References

[Getting started with Jenkins Configuration as Code](https://www.eficode.com/blog/start-jenkins-config-as-code)

[praqma-jenkins-casc](https://github.com/Praqma/praqma-jenkins-casc)

[Jenkins Configuration as Code (a.k.a. JCasC) Plugin](https://github.com/jenkinsci/configuration-as-code-plugin/blob/master/README.md)
