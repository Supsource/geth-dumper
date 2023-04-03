# geth-dumper

Geth-Dumper is a special purpose geth state dumper that performs several unique tasks to generate an initial OVM state with specific contract addresses. It does the following:

1. Deploys some initcode to a blank state
2. Creates a state dump
3. Replaces all instances of the initial contract addresses with some hardcoded addresses
4. Prints out the state dump

This tool is used for generating the initial OVM state (with an ExecutionManager & StateManager, etc) at specific addresses.

## Usage
Tested with go version go1.14.3 darwin/amd64.

### Generating State Dump Input (`deployment-tx-data.json`)
If you want to replace state dump input txs, you'll need to generate a new `deployment-tx-data.json` file. Do this when you make changes to the ExecutionManager and you'd like them reflected in the initial OVM state.

To generate a new deployment-tx-data.json file, follow these steps:
1. Find the Geth Input Dump test file [here.](https://github.com/ethereum-optimism/optimism)
2. Change `.skip` to `.only` in the test file to run the test and generate a `deployment-tx-data.json` file.
3. Copy the `deployment-tx-data.json` file into the root directory of this project.

### Generating a state dump
To generate a state dump, follow these steps:
1. Install Geth-Dumper with `go install`.
2. Run Geth-Dumper with `go run main.go`.
3. The tool will print out a lot of information.
4. Copy the dump hex from the output and paste it into `ovm_constants.go` in the L2Geth project.
5. The state dump is also saved in `state-dump.hex` (in hex format) and `state-dump.json` (in JSON string format) for your reference.

### Ingesting the state dump
You can ingest either the JSON version of the state dump or the hexified version of the state dump, depending on your preference.

## TODO
I'm actively working on making this process cleaner and more automated. Apologize for any inconvenience caused by the current tooling. Stay tuned for updates! Thank you for your understanding. Let's make the state dumping process even more beautiful! 🌟🚀😊
