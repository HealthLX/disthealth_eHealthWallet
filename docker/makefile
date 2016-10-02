#!/usr/bin/make -f

include makefile.config

.PHONY: debug default status stop

default: debug logs remove shell start status stop info

info:
	$(info $$var is [${TOP}, ${ipfs_staging}, ${ipfs_data}])

debug:
	docker run \
		--detach \
		--name $(name) \
		--volume $(ipfs_staging):/export \
		--volume $(ipfs_data):/data/ipfs \
		--publish 8080:8080 \
		--publish 4001:4001 \
		--publish 5001:5001 \
		--publish-all \
		$(image) \
		$(ARGS)

logs:
	docker logs --follow=true $(ARGS) $(name)

remove:
	docker rm --volumes=true $(ARGS) $(name)

shell:
	docker exec --interactive=true --tty=true $(name) /bin/login -f root -p $(ARGS)

start:
	docker start $(ARGS) $(name)

status:
	docker ps $(ARGS) --all=true --filter=name=$(name)

stop:
	docker stop $(ARGS) $(name)

