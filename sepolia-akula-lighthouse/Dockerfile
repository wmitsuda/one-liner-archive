FROM fedora:36 as builder

# base requirements
RUN dnf install -y git clang cmake e2fsprogs e2fsprogs-devel protobuf-compiler protobuf-devel

# rust toolchain
RUN curl --proto '=https' --tlsv1.2 -sSf https://sh.rustup.rs | sh -s -- -y
ENV PATH="$PATH:/root/.cargo/bin"

ENV GIT_COMMIT='57aeaa6f2709d3a04ae6b21b1bb5187b1adec496'
RUN git clone https://github.com/akula-bft/akula.git /akula
WORKDIR /akula

# checkout pinned akula commit; no stable tagged releases yet
RUN git checkout $GIT_COMMIT && cargo fetch
RUN cargo build --bin akula --profile=production

FROM fedora:36
RUN dnf install -y e2fsprogs
COPY --from=builder /akula/target/production/akula /usr/local/bin/akula

EXPOSE 8545 \
       8551 \
       30303 \
       30303/udp \
       42069 \
       42069/udp
