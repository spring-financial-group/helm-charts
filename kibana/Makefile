default: setup
include ../helpers/common.mk

RELEASE := elasticsearch-kibana
STACK_VERSION := 7.4.1

setup: secrets install

install:
	helm upgrade --install --namespace=jx --wait --timeout=600 --install --values ./values.yaml $(RELEASE) ./ ; \
  
secrets:
	encryptionkey=$$(echo $$(docker run --rm docker.elastic.co/elasticsearch/elasticsearch:$(STACK_VERSION) /bin/sh -c "< /dev/urandom tr -dc _A-Z-a-z-0-9 | head -c50")) && \
	kubectl create secret generic kibana --from-literal=encryptionkey=$$encryptionkey --namespace=jx
