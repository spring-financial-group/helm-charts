default: setup

include ../helpers/common.mk

RELEASE := elastic-search
STACK_VERSION := 7.4.1

setup: purge secrets install

secrets:
	docker rm -f elastic-helm-charts-certs || true
	rm -f elastic-certificates.p12 elastic-certificate.pem elastic-stack-ca.p12 || true
	password=$$([ ! -z "$$ELASTIC_PASSWORD" ] && echo $$ELASTIC_PASSWORD || echo $$(docker run --rm docker.elastic.co/elasticsearch/elasticsearch:$(STACK_VERSION) /bin/sh -c "< /dev/urandom tr -cd '[:alnum:]' | head -c20")) && \
	docker run --name elastic-helm-charts-certs -i -w /app \
		docker.elastic.co/elasticsearch/elasticsearch:$(STACK_VERSION) \
		/bin/sh -c " \
			elasticsearch-certutil ca --out /app/elastic-stack-ca.p12 --pass '' && \
			elasticsearch-certutil cert --name security-master --ca /app/elastic-stack-ca.p12 --pass '' --ca-pass '' --out /app/elastic-certificates.p12" && \
	docker cp elastic-helm-charts-certs:/app/elastic-certificates.p12 ./ && \
	docker rm -f elastic-helm-charts-certs && \
	openssl pkcs12 -nodes -passin pass:'' -in elastic-certificates.p12 -out elastic-certificate.pem && \
	kubectl create secret generic elastic-certificates --from-file=elastic-certificates.p12 --namespace jx && \
	kubectl create secret generic elastic-certificate-pem --from-file=elastic-certificate.pem --namespace jx && \
	kubectl create secret generic elastic-credentials  --from-literal=password=$$password --from-literal=username=elastic --namespace jx && \
	rm -f elastic-certificates.p12 elastic-certificate.pem elastic-stack-ca.p12
	

install:
	helm upgrade --namespace=jx --wait --timeout=600 --install --values ./values.yaml $(RELEASE) ./ ; \
	
purge:
	kubectl delete secrets --namespace jx elastic-credentials elastic-certificates elastic-certificate-pem || true
	helm del --purge $(RELEASE)
