FROM rust:latest AS builder

RUN apt-get update

RUN apt-get install -y \
    build-essential \
    curl

RUN apt-get update

RUN apt install make

RUN apt-get -y update

RUN apt-get -y install gcc git 

RUN apt-get -y update

RUN curl -y --proto '=https' --tlsv1.2 -sSf https://sh.rustup.rs | sh

RUN git clone https://github.com/cjdelisle/packetcrypt_rs --branch develop

WORKDIR packetcrypt_rs

RUN cargo build --release

FROM debian:buster

WORKDIR /

COPY --from=builder /packetcrypt_rs/target/release/packetcrypt .

COPY run.sh .

ENTRYPOINT [ "./run.sh" ]

