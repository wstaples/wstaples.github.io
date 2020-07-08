---
layout: post
title:  "Nomad Project"
date:   2016-10-02 18:34:28 -0400
categories: nomad
---

We are in need of a new development and deployment life cycle. 

suggested approach:

1. clone the empty laravel website from the git repo. This will contain docker files, laravel stuff and consul 
2. run docker-compose up -d
3. run docker exec -it <container_name> bash (from here you may run composer commands and such)
4. you may edit files outside your container (directly from the laravel folder like you do now)
5. your application must include:  
    1. one /health route (which is not a closure)  
	2. at least 1 unit test (which can just test your /health route)  
	3. a nomad job file  
	4. a yaml file describing your configuration and secrets  
6. develop as usual & commit as usual
7. when ready to deploy commit with a tag (on your dev branch)
8. jenkins will detect the tag and build a new docker image with your code baked in.
9. jenkins will test the created box and if the tests pass deploy to the dev nomad cluster
10. users may now test your application
11. if the application passes user testing (?? add the nomad job file to the nomad live repository ?? or maybe add a tag of some kind?)
12. perform canary deployment. if no errors replace all live instances. 



- ToDo
	- Setup a local consul server
	- setup a local vault server
	- method of loading stuff into consul & vault local servers
	- method of moving stuff from local servers to dev 
	- why is nano / vim messed up?
	- make sure containers can use aws resources
	- how do we deploy to live?
	- canary deployment
<br /><br />


#### Cloning the repo
1. Open a command window and cd into your project folder.
2. Run `git clone https://bitbucket.org/geiger-it/order_api`
3. Run `git remote rm origin`
4. Run `git remote add origin <your repo here>`
5. Run `git push --all origin -u`
<br /><br />


#### Begin Development
 **Everything must point to dev. Do not point anything to a live server or database**

1. Review and Edit the following files to meet your needs:
	- docker-compose
	- Dockerfile
	- laravel/composer.json
	- laravel/config/*.php
	- create env file `cp env.sample .env`
	- .gitingore
2. run `docker-compose down && docker-compose build && docker-compose up -d`
3. run `docker exec -it <container_name> bash` (from here you may run composer commands and such)
4. run `composer install`
5. develop as usual
6. when ready `git tag -a 1.0.0 -m "my version 1.0.0"`
<br /><br />


#### User Testing
1. after pushing a tagged revision watch for a pull request from our CI system.
2. pull request should contain the URL to the dev system
3. Optionally request CNAME from Evan and Brian
4. allow users to test
5. 




