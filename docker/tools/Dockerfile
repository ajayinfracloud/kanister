FROM registry.access.redhat.com/ubi8/ubi-minimal:8.1
ARG kan_tools_version="test-version"
LABEL name="kanister-tools" \
    vendor="Kanister" \
    version="${kan_tools_version}" \
    release="${kan_tools_version}" \
    summary="Microservice for application-specific data management for Kubernetes" \
    maintainer="Tom Manville<tom@kasten.io>" \
    description="Kanister tools for application-specific data management"

COPY --from=restic/restic:0.9.5 /usr/bin/restic /usr/local/bin/restic
# kopia alpine-bba1dcc image
COPY --from=kanisterio/kopia@sha256:9ce566a18b084b8cfa1ee63cfde8a37ebda8cd29bbf72f4489530ec2200aa2e2 /kopia/kopia /usr/local/bin/kopia
COPY LICENSE /licenses/LICENSE

ADD kando /usr/local/bin/
RUN microdnf update && microdnf install shadow-utils httpd-tools && \
  adduser -U kanister -u 1000 && \
  microdnf remove shadow-utils && \
  microdnf clean all

CMD [ "/usr/bin/tail", "-f", "/dev/null" ]
