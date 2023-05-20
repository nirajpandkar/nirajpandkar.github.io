---
title: "How to use a Dockerized PgAdmin and make user management easy"
date: 2019-12-15T17:12:39+05:30
draft: false

featured_image: "/images/pgadmin-docker.png"

tags: ['docker', 'pgadmin']
categories: ['DevOps']
toc: true
---

We interact with databases almost all day long - consuming video content on the largest streaming service, chatting with your friend on the most widely used chat application or just poking your friend on the most powerful social networking site. 

When a company's heart and soul rests in a database, as ours do at [Riverus](https://riverus.in/), it becomes mandatory to make it easily accessible not only to the engineering and data science team, but to the legal, sales and marketing team as well.

*At Riverus, we use PostgreSQL database system to store almost all the historical and latest judgement cases and provide insightful analytics on the same. PgAdmin is our heavily used gateway to interact with the database.*

## What to except from this article?

1. Using a Docker image created for pgAdmin with minimum side hustle and it's advantages.
2. In case of a server or docker application crash, how to retain user and server data.
3. My experience and learnings along the way.

### Motivation for this article

In the process of making pgAdmin available for everyone, I noticed that it took a significant amount of my time to setup and maintain user data. Also there was an added step for the users to setup their database credentials time and again whenever the application or server crashed.

### Purpose of this article

I did a bit of exploring and found out that user and server data was stored in an SQLite database which I could import while initializing the docker. For me it implied, executing one smooth docker command and voila! - instant access for the users with zero effort which was my ultimate goal.

# Why dockerized PgAdmin?

There are three reasons why I deemed it necessary to install a dockerized version of pgAdmin - 

1. Reinstalling and setting up the environment in case of a server crash was a pain in the bum area
2. It helps in isolating the installation environment and not mess with the already installed applications on the server
3. Less hassle to startup the application

With this I set out to write my own Dockerfile when I found that someone had already created a [comprehensive pgAdmin docker](https://github.com/fenglc/dockercloud-pgadmin4) (which is deprecated at the time of writing this article). I tried running this docker container and ran into some issues which I fixed and made some changes in the Dockerfile which is now hosted as a [fork here](https://github.com/nirajpandkar/pgadmin-docker). 

## Installing and hosting PgAdmin docker

Since the main focus of this blog is to educate the reader on the ease of access, I am not going to dive into installation. You'll find detailed instructions to setup docker and spin up a working PgAdmin container in my [README](https://github.com/nirajpandkar/pgadmin-docker/blob/master/README.md).

The next steps would be to host it on a server and make it available to the user. If you've got a working container up and running, you may have noticed that the application is running on port 5050. 

You can either forward port 5050 of your server or use a proxy server - [Nginx](http://tutorials.jenkov.com/nginx/index.html). I'll have a detailed article on this topic soon.

## Saving and importing user data

Once the users have setup their databases using their PgAdmin and database credentials for the first time, we can commence the wizardry. 

- **Copy the folder `/var/lib/pgadmin` residing in the running container to the host** (assuming you named your docker image 'riverus-pgadmin'; if not then change the command accordingly)

```
docker cp `docker ps | grep 'riverus-pgadmin' | awk '{ print $1 }'`:/var/lib/pgadmin /path/to/pgadmin-docker
```

You'll find a file called `pgadmin4.db` which is a sqlite database which stores all the user data including the servers created by the individual users inside their PgAdmin accounts as well as the query history per session. Additionally, you'll find a folder called `storage` which stores user saved queries.

**Note:** Don't forget to take a backup of this folder on your local machine or on your private git repositories (since it contains sensitive data)

- **Now let's say, the unspeakable happens and the application crashes or worse the server reboots. You just have to run this one docker command to restore the application and user data**

```
cd ~/pgadmin-docker && docker run -p 5050:5050 -d riverus-pgadmin && docker cp ./pgadmin `docker ps | grep 'riverus-pgadmin' | awk '{ print $1 }'`:/var/lib
```

This copies the whole `pgadmin` folder into the container after it starts. If you visit the webapp again, you'll see that all user data as well as stored queries is intact!

![Celebration](/images/celebration.gif)

## Future Scope

Instead of copying the data folder from the container to host and to the container again, the next step would be to build a docker image with the data folder integrated. If you are able to crack this, feel free to submit a [pull request](https://github.com/nirajpandkar/pgadmin-docker).