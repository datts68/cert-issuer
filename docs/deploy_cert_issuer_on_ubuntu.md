# Deploy cert-issuer on Ubuntu 16.04

### Clone the repo and change to the directory:
    git clone https://github.com/blockchain-certificates/cert-issuer.git && cd cert-issuer

### Install requirements:
    sudo apt install python3-pip python3-dev libssl-dev virtualenv

### I recommend using virtualenv to manage your python environments:
    pip3 install virtualenv
    virtualenv -p python3 venv

    # If you have a warning:
    # You are using pip version 8.1.1, however version 9.0.3 is available. You should consider upgrading via the 'pip install --upgrade pip' command.
    # You can run: 'pip3 install -U pip'

Activate the environment:

    source ./venv/bin/activate
    
After you’re finished, deactivate the environment by running:
    deactivate

### Install cert-issuer
By default, cert-issuer issues to the Bitcoin blockchain. Run the default setup script if this is the mode you want:

    python3 setup.py install

To issue to the ethereum blockchain, run the following:

    python3 setup.py experimental --blockchain=ethereum

### Configuring cert-issuer
Create your conf.ini file (the config file for this application):

    issuing_address = <issuing-address>

    chain=<bitcoin_regtest|bitcoin_testnet|bitcoin_mainnet|ethereum_testnet|ethereum_ropsten|ethereum_mainnet|mockchain>
    
    usb_name = </Volumes/path-to-usb/>
    key_file = <file-you-saved-pk-to>

    unsigned_certificates_dir=<path-to-your-unsigned-certificates>
    blockchain_certificates_dir=<path-to-your-blockchain-certificates>
    work_dir=<path-to-your-workdir>

    no_safe_mode

    # advanced: uncomment the following line if you're running a bitcoin node
    # bitcoind

Notes:
* The bitcoind option is technically not required in regtest mode. regtest mode only works with a local bitcoin node. The quick start in docker brushed over this detail by installing a regtest-configured bitcoin node in the docker container.
* The Ethereum option does not support a local (test)node currently. The issuer will broadcast the transaction via the Etherscan API.

### Install command cert-issuer
    pip3 install .

### Issuer
Add your certificates to data/unsigned_certs/.

Issue the certificates on the blockchain:

    cert-issuer -c conf.ini

Done!
