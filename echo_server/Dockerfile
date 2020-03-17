# Build 
FROM rust:1.42-alpine as build

RUN apk add --no-cache musl-dev

COPY ./ ./

ENV RUSTFLAGS="-C target-feature=-crt-static"
RUN cargo build --release

RUN mkdir -p /build-out

RUN cp target/release/echo_server /build-out/

# Run
FROM alpine

RUN apk add --no-cache gcc
COPY --from=build /build-out/echo_server /

CMD /echo_server