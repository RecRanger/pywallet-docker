# pywallet-docker
A Dockerfile for the Python 2 [pywallet tool](https://github.com/jackjack-jj/pywallet)

This guide provides instructions on how to build and run the `pywallet` application within a Docker container. `Pywallet` is a Python tool used for managing Bitcoin wallet files.

## Prerequisites

Before you begin, ensure that Docker is installed on your system. If not, follow the installation instructions for your respective operating system on the [Docker website](https://docs.docker.com/get-docker/) or [vpsbg.eu](https://www.vpsbg.eu/docs/docker-installation-on-vps-vds).

## Building the Docker Image

To build the Docker image, perform the following steps:

1. Open a terminal.
2. Navigate to the directory containing the Dockerfile (where this repo was cloned).
3. Run the following command to build the Docker image:

```bash
docker build -t pywallet-image .
```

This command builds an image named `pywallet-image` using the Dockerfile in the current directory.

## Running the Container

To run the `pywallet` application within the Docker container, use the following command:

```bash
docker run pywallet-image [arguments]
```

Replace `[arguments]` with the actual arguments you want to pass to `pywallet.py`.

## Examples

### Getting Help

To display the help information for `pywallet.py`, run:

```bash
docker run pywallet-image --help
```

### Working with Local Files

If you need to work with wallet files located on your local file system, you must mount the directory containing the files into the Docker container. Use the following command structure:

```bash
docker run -v /path/to/local/directory:/pywallet/data pywallet-image --datadir=/pywallet/data --dumpwallet
```

Replace `/path/to/local/directory` with the path to the directory on your local machine where your wallet files are stored.

### Recovering a Wallet

To recover a wallet using a wallet.dat file located on your local system:

```bash
docker run -v /path/to/local/directory:/pywallet/data pywallet-image --datadir=/pywallet/data --recover --recov_device=/pywallet/data/wallet.dat --recov_size=20Mio
```

Make sure to replace `/path/to/local/directory` with the actual path where your `wallet.dat` file is stored and adjust the `--recov_size` argument according to the estimated size of your wallet.

## Notes

- When mounting volumes (`-v` option), the path specified in the container (e.g., `/pywallet/data`) must correspond to the expected data directory path used within the `pywallet.py` application.
- Ensure that you use absolute paths both for the local directory on your host and within the container to avoid path resolution issues.

