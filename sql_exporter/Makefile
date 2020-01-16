# Copyright 2015 The Prometheus Authors
# Licensed under the Apache License, Version 2.0 (the "License");
# you may not use this file except in compliance with the License.
# You may obtain a copy of the License at
#
# http://www.apache.org/licenses/LICENSE-2.0
#
# Unless required by applicable law or agreed to in writing, software
# distributed under the License is distributed on an "AS IS" BASIS,
# WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
# See the License for the specific language governing permissions and
# limitations under the License.

# https://github.com/free/sql_exporter/blob/master/Makefile


# Transform the machine arch into some standard values: "arm", "arm64", or "amd64". 
# Note: ppc64le already returns ppc64le, so we do not need to change that.
SYSTEM_ARCH := $(shell uname -m | sed -e 's/aarch64.*/arm64/' -e 's/x86_64.*/amd64/' -e 's/armv.*/arm/')

# To build for an arch different from the current system, set this env var to 1 of the values in the comment above
ARCH ?= $(SYSTEM_ARCH)
DOCKER_NAME ?= sql_exporter
PORT_NUM ?= 9399

default: all

all: build run
	
run:
	docker run -p=$(PORT_NUM):$(PORT_NUM) --name="$(DOCKER_NAME)" $(DOCKER_NAME)

build:
	docker build -t $(DOCKER_NAME) -f ./Dockerfile.$(ARCH) .
	
# Stop and remove a running container
stop: 
	#docker stop $(DOCKER_NAME)
	docker stop $(DOCKER_NAME); docker rm $(DOCKER_NAME)

# Clean the container
clean:
	-docker rmi $(DOCKER_NAME) 2> /dev/null || :
	
test:
	echo 'test'
	
.PHONY: all run build stop clean