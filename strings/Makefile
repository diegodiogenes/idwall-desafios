NAME=formatter

.check-image-exists:
ifeq ($(shell docker images -q ${NAME}),)
	@docker build -t ${NAME} .
endif

.check-container-running:
ifeq ($(shell docker ps | grep ${NAME}),)
	@docker run --name ${NAME} --rm -d -it -v $(shell pwd)/outputs/:/app/outputs ${NAME}
endif

run: .check-image-exists .check-container-running
	@docker exec -it ${NAME} bash

test: .check-image-exists .check-container-running
	@docker exec -it ${NAME} python -m unittest discover tests

help: .check-image-exists .check-container-running
	@docker exec -it ${NAME} python main.py --help

example: .check-image-exists .check-container-running
	 @docker exec -it ${NAME} python main.py --input input.txt --path inputs --align justify
