BASE := ghcr.io/fillin-inc/go
TAG := 1.17-bullseye-slim
REPO := ${BASE}:${TAG}

repo:
	@echo ${REPO}

build:
	docker build -t ${REPO} .

size:
	docker images | grep ${BASE} | grep ${TAG} | awk '{print $$NF}'

push:
	docker push ${REPO}

local:
	docker run --rm -it ${REPO} bash
