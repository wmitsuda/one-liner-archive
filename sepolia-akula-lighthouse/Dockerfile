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

RUN git clone https://github.com/wmitsuda/akula.git /akula
WORKDIR /akula
RUN git checkout 9fb7ceb4f7edc6933a8c624e676afd8a1e0d29d2 && cargo fetch
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
