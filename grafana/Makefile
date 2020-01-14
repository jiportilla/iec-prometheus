# Make targets for building the IBM Edge Computing Prometheus container

# Transform the machine arch into some standard values: "arm", "arm64", or "amd64". 
# Note: ppc64le already returns ppc64le, so we do not need to change that.
SYSTEM_ARCH := $(shell uname -m | sed -e 's/aarch64.*/arm64/' -e 's/x86_64.*/amd64/' -e 's/armv.*/arm/')

# To build for an arch different from the current system, set this env var to 1 of the values in the comment above
ARCH ?= $(SYSTEM_ARCH)

# These variables can be overridden from the environment
PORT_NUM ?= 3000
DOCKER_NAME ?= iec-grafana

default: all

all: build run

# Build the docker image for the current architecture
build:
	docker build -t $(DOCKER_NAME) -f ./Dockerfile.$(ARCH) .
	
run:
	docker run -p=$(PORT_NUM):$(PORT_NUM) --name="$(DOCKER_NAME)" $(DOCKER_NAME)
	
# Stop and remove a running container
stop: 
	docker stop $(DOCKER_NAME); docker rm $(DOCKER_NAME)

# Clean the container
clean:
	-docker rmi $(DOCKER_NAME) 2> /dev/null || :

.PHONY: build run stop clean 