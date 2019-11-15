default: setup

RELEASE := fluentd
STACK_VERSION := 1.0.0

setup: install

docker:
	docker build --tag docker.pkg.github.com/spring-financial-group/helm-charts/fluentd:$(STACK_VERSION) --tag docker.pkg.github.com/spring-financial-group/helm-charts/fluentd:latest .
	docker push docker.pkg.github.com/spring-financial-group/helm-charts/fluentd:latest
	docker push docker.pkg.github.com/spring-financial-group/helm-charts/fluentd:$(STACK_VERSION)

install:
	helm upgrade $(RELEASE) --namespace=jx --wait --timeout=600 --install ./
	
purge:
	helm del --purge $(RELEASE)
