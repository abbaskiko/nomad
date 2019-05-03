.PHONY: image_internal
image_internal:
	docker build --pull  -t circleci/nomad:$(TAG) .

.PHONY: image_server
image_server:
	docker build \
		-t circleci/server-nomad:$(TAG) \
		--build-arg BASE_NOMAD_TAG=$(TAG) \
		-f ./Dockerfile.server .

.PHONY: publish
publish: image_internal image_server
	docker push circleci/nomad:$(TAG)
	docker push circleci/server-nomad:$(TAG)
