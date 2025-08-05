FROM busybox@sha256:f9a104fddb33220ec80fc45a4e606c74aadf1ef7a3832eb0b05be9e90cd61f5f AS source
# Create the data directory for eg
RUN mkdir -p /var/lib/eg

# Use distroless as minimal base image to package the manager binary
# Refer to https://github.com/GoogleContainerTools/distroless for more details
FROM gcr.io/distroless/base-nossl:nonroot@sha256:d1fc914c43cea489c26c896721344a49a1761b9bb678bcba1758772d22913302
ARG TARGETPLATFORM
COPY --chown=65532:65532 $TARGETPLATFORM/envoy-gateway /usr/local/bin/
COPY --from=source --chown=65532:65532 /var/lib /var/lib

USER 65532:65532

ENTRYPOINT ["/usr/local/bin/envoy-gateway"]
