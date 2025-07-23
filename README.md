# Overview

Using burn libraries with cuda (gpu) to train and infer a metrics data set 

## Usage

**N.B.**  The data for training, validating and testing is proprietary and has not 
been included in this repo for obvious reasons.

The DataLoader will look for files named

- data/metrics-100000.csv (used for training)
- data/metrics-20000.csv (used for validating)
- data/metrics-1000.csv (used for testing)

Change the directories and file names before compiling.

clone the repo

```bash
cd rust-burn-metrics

# build 

cargo build --release

#execute (train)

./target/release/rust-burn-metrics --config app-config.json train

# execute (inference)

./target/release/rust-burn-metrics --config app-config.json inference

# execute (serve)

./target/release/rust-burn-metrics --config app-config.json serve


 # create a simple json file to check the prediction
cat <<EOF > metrics.json 
{
  "cpu": 22.3,
  "memory": 54.5,
  "disk": 12.9,
  "qtime": 43.9,
  "status": 1
}

curl -k -d'&metrics.json' https://localhost:8085/inference


```

## Certs

A script is included to create the key pairs for this service (tls)

It will copy a rootCA.pem file and update the local CA trust

N.B. Update the script (i.e -subj section to your requirments). The script is "fedora" specific, change it for your distro (espescially the trusted CA location)

Execute it with the following parameters

scripts/create-key-pair.sh <hostname> <ip>

