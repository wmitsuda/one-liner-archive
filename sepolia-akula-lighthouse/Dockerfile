FROM fedora:36 as builder

# base requirements
RUN dnf install -y git clang cmake e2fsprogs e2fsprogs-devel

# node (for otterscan build)
RUN curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.39.1/install.sh | bash
RUN export NVM_DIR="$HOME/.nvm" && [ -s "$NVM_DIR/nvm.sh" ] && \. "$NVM_DIR/nvm.sh" && nvm install 16.3
ENV PATH="$PATH:/root/.nvm/versions/node/v16.3.0/bin"

# rust toolchain
RUN curl --proto '=https' --tlsv1.2 -sSf https://sh.rustup.rs | sh -s -- -y
ENV PATH="$PATH:/root/.cargo/bin"

RUN git clone https://github.com/akula-bft/akula.git /akula
WORKDIR /akula

# checkout pinned akula commit; no stable tagged releases yet
RUN git checkout 8d00b15be8ed791b82f1a342b36e7ab823744a35 && cargo fetch
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
