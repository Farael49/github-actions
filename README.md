# github-actions
An example of a Maven & Docker based project using GitHub actions 

For this one, we'll reuse the already created maven-based jar generation, which we'll simply put in a docker image and publish to GitHub.

Relevant Sources :

- GitHub Docker Publish example :

https://github.com/actions/starter-workflows/blob/master/ci/docker-publish.yml

- Multiple examples of building Docker images w/ Spring :

https://spring.io/guides/gs/spring-boot-docker/

- Deeper dive on how to properly build a Java image, and a full docker setup (with maven builder, not needed here as GitHub Actions are building the jar) :

https://codefresh.io/docker-tutorial/java_docker_pipeline/
