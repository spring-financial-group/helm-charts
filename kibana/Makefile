default: setup
include ../helpers/common.mk

RELEASE := elasticsearch-kibana

setup: secrets install

install:
	helm upgrade --wait --timeout=600 --install --values ./values.yaml $(RELEASE) ./ ; \
  
 secrets:
	encryptionkey=$$(echo $$(docker run --rm docker.elastic.co/elasticsearch/elasticsearch:$(STACK_VERSION) /bin/sh -c "< /dev/urandom tr -dc _A-Z-a-z-0-9 | head -c50")) && \
	kubectl create secret generic kibana --from-literal=encryptionkey=$$encryptionkey
