# upstream-registry-builder v1.26.2
FROM quay.io/operator-framework/upstream-registry-builder@sha256:dc3ef48c8f6d90ea9654cd2ac5e32afbb777d6395b29f55f9976b201b62e4145 as builder

COPY manifests manifests
RUN ./bin/initializer -o ./bundles.db
############ ME
FROM scratch
COPY --from=builder /etc/nsswitch.conf /etc/nsswitch.conf
COPY --from=builder /bundles.db /bundles.db
COPY --from=builder /bin/registry-server /registry-server
COPY --from=builder /bin/grpc_health_probe /bin/grpc_health_probe
########## ME
EXPOSE 50051
ENTRYPOINT ["/bin/registry-server"]
CMD ["--database", "/bundles.db"]
