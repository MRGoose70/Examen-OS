# Stage 1: Build
FROM gcc:latest as builder

WORKDIR /usr/src/quark

COPY ./quark/quark .

RUN make

# Stage 2: Run
FROM debian

WORKDIR /app

COPY --from=builder /usr/src/quark/quark /usr/local/bin/quark

EXPOSE 8000

VOLUME /app

CMD ["quark", "-p", "8000", "-d", "/app"]