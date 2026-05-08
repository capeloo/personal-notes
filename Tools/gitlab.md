GitLab is a complete **DevOps platform** on which you build your complete DevOps workflows. One of the core parts of DevOps is **CI/CD** which has full support in GitLab. One of the benefits of using GitLab CI/CD over others like Jenkins is that you already have your code on GitLab.  

It has seamless integration into the code repository, without **the** overhead of setting it up yourself, and the pipeline configuration is part of your application code. Furthermore, you can self-host it or **use its managed SaaS**. 

---**Using self-hosted GitLab to create a CI/CD pipeline for a demo app PoC**---------------

Step-by-step process
- Install Docker and Docker Compose
- Make a new directory
- Create a docker-compose.yml file

![[gitlab-01.png]]

- Run "docker compose up -d"

![[gitlab-02.png]]

- Run "docker exec gitlab bash -c "cat /etc/gitlab/initial_root_password"" to get the root password

- After the first sign-in go in edit profile > access > password and authentication, to change password 

- Change configuration in settings > general > import and export settings, to allow import repository by URL 

- Import demo app (https://github.com/benc-uk/python-demoapp)

![[gitlab-03.png]]

- Clone locally too for testing and debug before creating the CI pipeline, make sure that the app can run (make test and make run)

![[gitlab-04.png]]

![[blog/assets/gitlab-evidences/gitlab-05.png]]

- Create a new file ".gitlab-ci.yml"

![[gitlab-06.png]]

- Now, to run the pipeline tests, a runner is required. A runner is simply a server or a server instance responsible for executing the jobs. For this, we will run a Docker container called `gitlab-runner`. The official image is available on Docker Hub. 
  
- Run "docker run -d --name gitlab-runner --restart always \  
	--network gitlab_default \  
	-v gitlab-runner-config:/etc/gitlab-runner \  
	-v /var/run/docker.sock:/var/run/docker.sock \  
	gitlab/gitlab-runner:latest"

- Now you have to register the runner on the project. To do this, run the following command: "docker exec -it gitlab-runner gitlab-runner register"

- During the registration process, GitLab Runner will ask for some information:
		- **GitLab instance URL**  
	    Use the URL of your GitLab instance: "http://gitlab"
	    - **Registration token**  
		You can find this token in your GitLab project under: Settings > CI/CD > Runners
		- **Description**  
		Choose a name for your runner, for example: local-gitlab-runner
		- **Tags**  
		Optional tags to identify the runner: docker,python
		- **Default Docker image**  
		Define the default image used by the jobs: python:3.9-slim

- After the registration is completed, restart the runner container: "docker restart gitlab-runner". The runner should appear with the status online

![[gitlab-07.png]]

- Now, after some debugging and configuration fixes, the jobs in the pipeline should run successfully

![[gitlab-08.png]]

- 