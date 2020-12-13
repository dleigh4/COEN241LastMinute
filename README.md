[//]: # (SPDX-License-Identifier: CC-BY-4.0)

# COEN 241 Project: Team Last Minute

This project makes use of Hyperledger's Fabric sample library, and requires its installation and compilation.

# Downloading and building the sample library

Linux prerequisites: git, curl, Docker + Docker Compose
Other systems: see [the documentation page](https://hyperledger-fabric.readthedocs.io/en/release-2.2/prereqs.html)

With curl, run 
**curl -sSL https://bit.ly/2ysbOFE | bash -s
to clone the sample repository and install the latest necessary binaries for Hyperledger Fabric and Hyperledger CA.
 
 For full steps, see [the documentation page](https://hyperledger-fabric.readthedocs.io/en/release-2.2/install.html).

# Setting up the testing environment

Using a file manager, open the **fabric-samples** directory. Delete the **high-throughput** directory and its contents, and then replace it with the **high-throughput** directory and contents included in this project's root.

Similarly, in **fabric-samples/test-network**, replace the **docker** directory and its contents with the included **docker** directory in this project's root. Additionally, in the **fabric-samples/test-network** folder, copy in the **peer1enroll.sh** and **peer2enroll.sh** script files.

# Run the environment

From a terminal window, while within the **fabric-samples** directory, add the Fabric to the execution path and set its environmental variable using:
**export PATH=${PWD}/../bin:$PATH**
**export PATH=${PWD}/../bin:$PATH**

Do this for any terminal instance operating on the test network.

Within the **fabric-samples/high-throughput** directory, run
**./startFabric.sh**
to bring up the Fabric and basic containers (CAs, manager, 2 peer nodes).

Within the **fabric-samples/high-throughput/application-go** directory, run
**go run app.go manyUpdates testvar1 100 +**
to submit 1000 simultaneous updates to add 100 to object testvar1 to the network.

To bring down the network, from within **fabric-samples/high-throughput**, run
**./networkDown.sh**

To adjust resource allocation, change the corresponding **cpu** and **mem_limit** environmental variables for peer0.org1 and peer0.org2 within **fabric-samples/test-network/docker/docker-compose-test-net.yaml**

# Adjusting for more nodes

To generate cryptographic material for the two additional peer nodes included, from **fabric-samples/test-network**, run
**./peer1enroll.sh**
to generate material for peer1 of org 1, and

**./peer2enroll.sh**
to generate material for peer2 of org 1.


To bring up the containers, from within **fabric-samples/test-network**, run
**docker-compose -f docker/docker-compose-peer1org1.yaml up -d**
for peer1 of org 1, and

**docker-compose -f docker/docker-compose-peer2org1.yaml up -d**
for peer2 of org 2.

