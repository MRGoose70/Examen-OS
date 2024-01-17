# Stage 1: Build
FROM gcc:latest as builder

WORKDIR /usr/src/quark

COPY ./quark/quark .

RUN make

# Stage 2: Run
FROM debian

WORKDIR /app/root

COPY --from=builder /usr/src/quark/quark /usr/local/bin/quark

EXPOSE 8080

VOLUME /app/root

CMD ["quark", "-h", "0.0.0.0", "-p", "8080", "-d", "/app/root"]