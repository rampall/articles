# Build on Swarm: Running a Bee Node for Testing and Development

Running a Bee node is essential for building decentralized applications on the Swarm network. However, as a developer, it is often convenient to work in an environment where interactions with the node/network can be tested rapidly and without putting the node’s storage data or the user’s tokens at risk. 

In this article, we'll explore 3 safe and risk-free options available for developers to run a Bee node on Swarm primarily for testing and development:

1. Run Bee in developer mode
3. Run a local network with Bee Factory
4. Run a local network with FDP Play

Whether you're a beginner or an experienced developer, these options will help you get started with Swarm quickly. So let's dive in!

## Option 1: Run Bee in Developer Mode

When a Bee node is started in developer mode, it creates an instance with volatile persistence and all back-ends mocked. This mode is highly advantageous for testing and experimenting with various Bee node features and capabilities, as any changes made are temporary and discarded when the node is stopped. As a result, there is no impact on real-world data or assets, making this mode an ideal option for developers looking to experiment with the Bee node.

### Prerequisites

* ports `1633` and `1635` must be free and available

### Step 1: Install `bee` on your system

You can install the [latest bee version](https://github.com/ethersphere/bee/releases/latest) on your system:

1. Using [Installer packages](https://docs.ethswarm.org/docs/installation/install)
    * Ubuntu/Debian (*.deb)
    * CentOS (*.rpm)
    * MacOS (brew)

2. Using the [installer script](https://docs.ethswarm.org/docs/installation/manual) which automatically detects your execution environment and installs the latest stable version of `bee` on your computer
    * Linux (bee-linux-*)
    * MacOS (bee-darwin-*)
    * Windows (bee-windows-*)

3. Directly [building from the source](https://docs.ethswarm.org/docs/installation/build-from-source) on other unsupported systems.

### Step 2: Start Bee in `dev` mode

Open a terminal window and run:
```
bee dev
```

```
 (                      *        )  (
 )\ )                 (  *    ( /(  )\ )
(()/(   (    (   (    )\))(   )\())(()/(   (
 /(_))  )\   )\  )\  ((_)()\ ((_)\  /(_))  )\
(_))_  ((_) ((_)((_) (_()((_)  ((_)(_))_  ((_)
 |   \ | __|\ \ / /  |  \/  | / _ \ |   \ | __|
 | |) || _|  \ V /   | |\/| || (_) || |) || _|
 |___/ |___|  \_/    |_|  |_| \___/ |___/ |___|


Starting in development mode

"time"="2023-03-08 13:55:59.008839" "level"="info" "logger"="node/localstore" "msg"="database capacity" "chunks"=1000000 "~size(GB)"=20.29025
"time"="2023-03-08 13:55:59.008726" "level"="info" "logger"="node" "msg"="starting debug api server" "address"="[::]:1635"
"time"="2023-03-08 13:55:59.022163" "level"="info" "logger"="node" "msg"="starting api server" "address"="[::]:1633"

```

Great! Our bee node is now running in `dev` mode. You can now safely interact with all of its API endpoints. Any changes to the node's state resulting from your interactions will only be persisted to memory.

## Option 2: Run a local network with Bee Factory

[Bee Factory](https://github.com/ethersphere/bee-factory) offers a complete solution to simulate an entire Swarm Network on your machine. Bee Factory is a CLI tool to spin up a Docker cluster of Bee nodes as well as a test Blockchain for advanced testing and development.

### Prerequisites

* Docker must be already installed
* `node` >= `16`
* ports `1633` and `1635` must be free and available

### Step 1: Install Bee Factory

```
npm install -g @ethersphere/bee-factory
```

### Step 2: Using Bee Factory

Spin up the cluster for a specific Bee version and attached to the Queen bee node logs (Press Ctrl+C to stop)

```
bee-factory start 1.11.1
```

Or spin up the cluster for a specific Bee version, detach and exit

```
bee-factory start --detach 1.11.1
```


Stop a running bee cluster


```
bee-factory stop
```


To delete existing containers while switching versions, you can use the `–-fresh` flag


```
bee-factory start 1.11.0 --fresh
```

To list all available subcommands


```
bee-factory --help
```


To list help content for a specific subcommand


```
bee-factory <subcommand> --help
```
:::info
You can check out [https://github.com/ethersphere/bee-factory](https://github.com/ethersphere/bee-factory) for more information on `bee-factory`.
:::


## Option 3: Run a local network with FDP Play

[Fair Data Protocol](https://fdp.fairdatasociety.org/) (FDP) is a data interoperability protocol and a layer 2 solution built on top of Swarm. It promotes self-sovereignty and privacy for dApps that use personal data in the decentralized cloud.

Much like the `bee-factory`,[FDP Play](https://github.com/fairDataSociety/fdp-play) is a CLI tool to spin up a local development FDP environment with Docker. It includes a ganache blockchain for testing, a Docker cluster of bee nodes as well as a FairOS instance.

### Prerequisites

* Docker must be already installed
* `node` >= `16`
* ports `1633`, `1635` and `9090` must be free and available

### Step 1: Install FDP Play

```
npm install -g @fairdatasociety/fdp-play
```

### Step 2: Using FDP Play

Start a bee cluster using the latest supported Bee version.

```
fdp-play start
```

Start a bee cluster for specific Bee version and exit.


```
fdp-play start -d --bee-version 1.11.1
```

Attach to the Queen container and displays its logs

```
fdp-play logs queen --follow
```

Stop the cluster (container data persists between restarts)

```
fdp-play stop
```

Clear all data (fresh) and pull latest docker images

```
fdp-play start --pull --fresh
```

Spin up the cluster using specific blockchain image

```
fdp-play start --detach --blockchain-image fairdatasociety/fdp-play-blockchain
```
:::info
You can check out [https://github.com/fairDataSociety/fdp-play](https://github.com/fairDataSociety/fdp-play) for more information on `fdp-play`.
:::

# Alright, what's next?

Now that we've explored the three risk-free options to get a bee node running, it's time to start interactiong with it and building on the Swarm network. The [Bee JS](https://github.com/ethersphere/bee-js) SDK and its [documentation](https://bee-js.ethswarm.org/docs/) is a great place to get started next.

Check out our growing list of [free and open-source projects](https://github.com/ethersphere/awesome-swarm) related to Swarm and its ecosystem. Join the #develop-on-swarm channel on [Discord](https://discord.ethswarm.org/) to connect with other developers in the Swarm community. If you have a great idea that can make an impact, consider [applying for a grant](https://my.ethswarm.org/grants). The Swarm is waiting for *you*!