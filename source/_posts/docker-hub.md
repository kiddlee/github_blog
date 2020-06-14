---
layout: post
title: "Docker Hub"
date:   2016-01-18
description: Docker Hub
categories: Docker
tags: docker
---

After create docker image, I want to push image to docker hub to using next time easy. I should do as follow:

* Need to make sure I login docker hub

	```
	docker login --username=<YOUR_USERNAME> --email=<YOUR_EMAIL>
	```
	It will save login credentials in $HOME/.docker/config.json
* Create tag for image

    ```
    docker tag <IMAGE ID> <USERNAME>/<IMAGE NAME>
    ```

* Push image

    ```
    docker push <USERNAME>/<IMAGE NAME>
    ```

And then, you can pull you image everywhere(with VPN in some place).
