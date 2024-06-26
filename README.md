## Welcome to Optimism Package
default package for Optimism
```yaml
optimism_package:
  participants:
    - el_type: op-geth
      cl_type: op-node
ethereum_package:
  participants:
    - el_type: geth
    - el_type: reth
  network_params:
    preset: minimal
  additional_services:
    - dora
    - blockscout
```


## Configuration

To configure the package behaviour, you can modify your `network_params.yaml` file. The full YAML schema that can be passed in is as follows with the defaults provided:

```yaml
optimism_package:
  # Specification of the optimism-participants in the network
  participants:
    # EL(Execution Layer) Specific flags
      # The type of EL client that should be started
      # Valid values are op-geth, op-reth
    - el_type: geth

      # The Docker image that should be used for the EL client; leave blank to use the default for the client type
      # Defaults by client:
      # - op-geth: us-docker.pkg.dev/oplabs-tools-artifacts/images/op-geth:latest
      # - op-reth: parithoshj/op-reth:latest
      el_image: ""

    # CL(Consensus Layer) Specific flags
      # The type of CL client that should be started
      # Valid values are op-node, ?
      cl_type: op-node

      # The Docker image that should be used for the CL client; leave blank to use the default for the client type
      # Defaults by client:
      # - op-node: parithoshj/op-node:v1
      cl_image: ""

      # Count of nodes to spin up for this participant
      # Default to 1
      count: 1

  # Default configuration parameters for the network
  network_params:
    # Network name, used to enable syncing of alternative networks
    # Defaults to "kurtosis"
    # You can sync any public network by setting this to the network name (e.g. "mainnet", "sepolia", "holesky")
    # You can sync any devnet by setting this to the network name (e.g. "dencun-devnet-12", "verkle-gen-devnet-2")
    network: "kurtosis"

    # The network ID of the network.
    network_id: "2151908"

    # Seconds per slots
    seconds_per_slot: 2

  # Additional services to run alongside the network
  # Defaults to []
  # Available services:
  # - blockscout
  additional_services: []
```

### Additional configuration recommendations

It is required you to launch an L1 Ethereum node to interact with the L2 network. You can use the `ethereum_package` to launch an Ethereum node. The `ethereum_package` configuration is as follows:

```yaml
optimism_package:
  participants:
    - el_type: op-geth
      cl_type: op-node
  additional_services:
    - blockscout
ethereum_package:
  participants:
    - el_type: geth
    - el_type: reth
  network_params:
    preset: minimal
  additional_services:
    - dora
    - blockscout
```
