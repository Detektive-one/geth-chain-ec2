FROM ethereum/client-go:v1.13.15

# Create a password file
RUN echo "shiya123456789" > /ethereum_password.txt

# Copy genesis.json
COPY genesis.json /genesis.json

# Create the data directory structure
RUN mkdir -p /ethereum/keystore

# Copy the keystore file (ensure it's the full keystore file, not just a part)
COPY data/keystore/* /ethereum/keystore/

# Initialize the chain
RUN geth --datadir /ethereum init /genesis.json

# Expose RPC and WebSocket ports
EXPOSE 8545
EXPOSE 8546

# Entry point to run Geth
ENTRYPOINT ["geth", \
    "--datadir", "/ethereum", \
    "--networkid", "1337", \
    "--http", \
    "--http.addr", "0.0.0.0", \
    "--http.port", "8545", \
    "--http.api", "eth,net,web3,personal,clique", \
    "--http.corsdomain", "*", \
    "--ws", \
    "--ws.addr", "0.0.0.0", \
    "--ws.port", "8546", \
    "--ws.api", "eth,net,web3,personal", \
    "--ws.origins", "*", \
    "--unlock", "0", \
    "--password", "/ethereum_password.txt", \
    "--allow-insecure-unlock", \
    "--mine", \
    "--miner.etherbase", "0x25603C9E305e6720a6333279dd0D52A0e442AB46", \
    "--nodiscover"]
