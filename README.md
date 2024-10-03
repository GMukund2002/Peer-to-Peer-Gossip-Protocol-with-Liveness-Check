# Peer-to-Peer-Gossip-Protocol-with-Liveness-Check

## Description:
This project implements a peer-to-peer (P2P) gossip protocol network with liveness checks, designed to simulate a resilient, decentralized communication model. This system is built using Python and utilizes TCP sockets to manage communication between nodes in the network. The network consists of two types of nodes: seed nodes and peer nodes.

**Seed Nodes** serve as entry points to the network, helping new peers join by providing information about existing peers. They also keep track of dead nodes and ensure that information is always up-to-date for peers trying to connect.

**Peer Nodes** establish communication with both seeds and other peer nodes to form a connected graph. The peer nodes use a gossip protocol to broadcast messages and periodically check for the liveness of their connected peers.

## Features Implemented:
####  1.Gossip Protocol Implementation:

* Each peer generates and broadcasts a gossip message every 5 seconds. The messages are in the format <self.timestamp>:<self.IP>:<self.Msg#>.
* Gossip messages are forwarded through a network of peers, ensuring each peer gets the message at least once, while maintaining efficiency by avoiding redundant transmissions.
#### 2. Liveness Check:

* Peer nodes periodically (every 13 seconds) check the liveness of all peers they are connected to.
* If no response is received for 3 consecutive liveness requests, the node is reported as dead to the connected seeds.
#### 3.Connected Network:

* The network of peers forms a connected graph, where each peer randomly connects to a subset of other peers, ensuring redundancy and robustness.
* On startup, each peer connects to floor(n/2) + 1 randomly chosen seed nodes from a list provided in the config.txt file.
#### 4. Node Failure Management:

* Seed nodes maintain an updated list of connected peers. If a peer node is found to be dead, the corresponding seeds update their list and stop providing its information to new peers.
* When a peer identifies another peer as dead, it informs all associated seed nodes to ensure the list of active nodes is up-to-date.
#### 5.Multi-threading:

* The system is implemented using Python’s threading library to handle multiple tasks simultaneously, such as managing connections, broadcasting gossip messages, and handling liveness checks, thereby making the system efficient and responsive.
## File Descriptions:
* **seed.py**: Implements the seed node logic. Seeds maintain a list of all connected peers, handle incoming peer registrations, and update the peer list based on dead node reports.
* **peer.py**: Implements the peer node logic. Peers connect to seeds to get the network information, form connections with other peers, manage gossip message broadcasting, and perform liveness checks.
* **config.txt**: Contains a list of IP addresses and ports for all available seed nodes.
* **outputseed.txt**: Records all the output related to seed nodes, such as connection requests from peers and dead node notifications.
* **outputpeer.txt**: Records all the output related to peer nodes, such as gossip messages received, liveness checks, and dead node reports.


## Installation and Setup Instructions:
#### 1. Clone the Repository:
```bash
$ git clone https://github.com/username/peer-to-peer-gossip.git
$ cd peer-to-peer-gossip

Configure Seed Nodes:

Modify the config.txt file to include the IP addresses and ports of the available seed nodes.
Each line should have the format IP:Port, e.g., 172.30.21.114:8000
