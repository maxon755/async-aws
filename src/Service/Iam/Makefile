.EXPORT_ALL_VARIABLES:

initialize: start-docker
start-docker:
	docker start async_aws_localstack && exit 0 || \
	docker start async_aws_localstack-iam && exit 0 || \
	docker pull localstack/localstack:0.14.2 && \
	docker run -d -p 4572:4566 -e SERVICES=iam -v /var/run/docker.sock:/var/run/docker.sock --name async_aws_localstack-iam localstack/localstack:0.14.2 && \
	docker run --rm --link async_aws_localstack-iam:localstack martin/wait -c localstack:4566

test: initialize
	./vendor/bin/simple-phpunit

clean: stop-docker
stop-docker:
	docker stop async_aws_localstack-iam || true
