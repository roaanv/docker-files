NAME := java8-dev
DOCKER_HOST ?= unseen:6088/
DOCKER_USER ?= roaanv/
TAG ?= :latest
IMAGE_NAME = $(DOCKER_HOST)$(DOCKER_USER)$(NAME)$(TAG)
CONTAINER_NAME=$(NAME)

all: build

build: image

image:
	docker build -t $(IMAGE_NAME) .

run_docker: set_daemon container_runner

test_docker: container_runner

container_runner: stop
	-docker run --name $(CONTAINER_NAME) \
    	$(DAEMON_ARG) \
        $(IMAGE_NAME)

	-@sleep 2
	-@docker ps | grep $(CONTAINER_NAME)

set_daemon:
	$(eval DAEMON_ARG=-d)

shell:
	docker run -it $(IMAGE_NAME) /bin/bash

stop:
	-docker stop $(CONTAINER_NAME)
	-docker rm $(CONTAINER_NAME)

logs:
	-@docker logs $(CONTAINER_NAME)

push: image
	docker push $(IMAGE_NAME)

