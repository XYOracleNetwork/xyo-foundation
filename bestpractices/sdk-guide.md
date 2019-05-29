# SDK GUIDE

The following is a document to help you create a consistent sdk guide in the XYO suite of products.

SDKs are at the core of the functionality of applications, nodes, and other software services in XYO. 

There are shared elements of SDKs that should be documented across readmes and getting started guides. Getting Started Guides would share exact public functions across language and platform.

## Example Getting Started Guides for Core Swift and Kotlin Libraries

### sdk-core-kotlin

[![](https://jitpack.io/v/XYOracleNetwork/sdk-core-kotlin.svg)](https://jitpack.io/#XYOracleNetwork/sdk-core-kotlin) [![](https://img.shields.io/gitter/room/XYOracleNetwork/Stardust.svg)](https://gitter.im/XYOracleNetwork/Dev) [![Maintainability](https://api.codeclimate.com/v1/badges/af641257b27ecea22a9f/maintainability)](https://codeclimate.com/github/XYOracleNetwork/sdk-core-kotlin/maintainability) [![Test Coverage](https://api.codeclimate.com/v1/badges/af641257b27ecea22a9f/test_coverage)](https://codeclimate.com/github/XYOracleNetwork/sdk-core-kotlin/test_coverage)

[![](https://travis-ci.org/XYOracleNetwork/sdk-core-kotlin.svg?branch=master)](https://travis-ci.org/XYOracleNetwork/sdk-core-kotlin) [![BCH compliance](https://bettercodehub.com/edge/badge/XYOracleNetwork/sdk-core-kotlin?branch=master)](https://bettercodehub.com/) [![Sonarcloud Status](https://sonarcloud.io/api/project_badges/measure?project=XYOracleNetwork_sdk-core-kotlin&metric=alert_status)](https://sonarcloud.io/dashboard?id=XYOracleNetwork_sdk-core-kotlin) [![Known Vulnerabilities](https://snyk.io/test/github/XYOracleNetwork/sdk-core-kotlin/badge.svg)](https://snyk.io/test/github/XYOracleNetwork/sdk-core-kotlin)

Table of Contents

-   [Title](#sdk-core-kotlin)
-   [Long Description](#long-description)
-   [Read the Yellow Paper](#read-the-yellow-paper)
-   [Getting Started](#getting-started)
-   [Installing](#installing)
-   [Building and Testing with Gradle](#building-and-testing-with-gradle)
-   [License](#license)
-   [Credits](#credits)

## Long Description

A library to preform all core XYO Network functions.
This includes creating an origin chain, maintaining an origin chain, negotiations for talking to other nodes, and other basic functionality.
The library has heavily abstracted modules so that all operations will work with any crypto, storage, networking, etc.

## Read the Yellow Paper

The XYO protocol for creating origin-blocks is specified in the [XYO Yellow Paper](https://docs.xyo.network/XYO-Yellow-Paper.pdf). In it, it describes the behavior of how a node on the XYO network should create Bound Witnesses. Note, the behavior is not coupled with any particular technology constraints around transport layers, cryptographic algorithms, or hashing algorithms.

[Here](https://github.com/XYOracleNetwork/spec-coreobjectmodel-tex) is a link to the core object model that contains an index of major/minor values and their respective objects.

## Getting Started

Change your gradle file and add our dependency

For build instructions - [click here to go to the repo](https://github.com/XYOracleNetwork/sdk-core-kotlin)

[Click here for our sdk package](https://jitpack.io/#XYOracleNetwork/sdk-core-kotlin)

**You should start by setting up an interface to this library through creating an origin chain creator object.**

> Through an origin chain creator object one can create and maintain an origin chain. 

```kotlin
val originChain = XyoOriginChainCreator(blockRepo, stateRepo, hash)
```

```kotlin
// a key value store to store persist state and bound witnesses
val storage = XyoInMemoryStorageProvider()

// a hash implementation for the node to hash with
val hasher = XyoBasicHashBase.createHashType(XyoSchemas.SHA_256, "SHA-256")

// a place to store all off the blocks that the node makes
val blockRepo = XyoStorageOriginBlockRepository(storage, hasher)

// a place to store all of the origin state (index, keys, previous hash)
val stateRepo = XyoStorageOriginStateRepository(storage)

// the node object to create origin blocks
val node = XyoOriginChainCreator(blockRepo, stateRepo, hasher)
```

After creating a node, it is standard to add a signer, and create a genesis block.

```kotlin
// creates a signer with a random private key
val signer = XyoSha256WithSecp256K.newInstance()
    
// adds the signer to the node
node.originState.addSigner(signer: signer)

// creates a origin block with its self (genesis block if this is the first block you make)
node.selfSignOriginChain()
```

After creating a genesis block, your origin chain has officially started. Remember, all of the state is stored in the state repository (`XyoOriginChainStateRepository`) and the block repository (`XyoOriginBlockRepository`) that are constructed with the node. Both repositories are very high level and can be implemented for ones needs. Out of the box, this library comes with an implementation for key value store databases (`XyoStorageOriginBlockRepository`) and (`XyoStorageOriginChainStateRepository`). The `XyoStorageProvider` interface defines the methods for a simple key value store. There is a default implementation of an in memory key value store that comes with this library (`XyoInMemoryStorage`).

### Creating Origin Blocks

After a node has been created, it can be used to create origin blocks with other nodes. The process of talking to other nodes has been abstracted through use of a pipe (e.g. tcp, ble, memory) that handles all of the transport logic. This interface is defined as `XyoNetworkPipe`. This library ships with a and a tcp client and server pipe.

#### Using a TCP Pipe

**Client**

```kotlin
// creates a socket with the peer
val socket = Socket("myarchivist.com", 11000)

// creates a pipe so that we can send formated data through the socket
val pipe = XyoTcpPipe(socket, null)

// create a handler so that we can do the starting handshake with the node
val handler = XyoNetworkHandler(pipe)

// create the bound witness with the node on the socket
val newBoundWitness = node.boundWitness(handler, testProcedureCatalogue).await()
```

**Server**

```kotlin
// create a tcp server on port 11000
val server = XyoTcpServer(11000)

// listen from the server for connection events
server.listen { pipe ->
	// put bound witness into new thread (optional)
	GlobalScope.launch {
	
		// create a handler so that we can do the starting handshake with the node
	    	val handler = XyoNetworkHandler(pipe)
		
		// do the bound witness with the node
	    	val newBoundWitness = nodeTwo.boundWitness(handler, XyoBoundWitnessCatalog).await()
	}
}
```

Further examples of interacting through a socket can be found [here](https://github.com/XYOracleNetwork/sdk-core-kotlin/blob/feature/getting-started/src/test/kotlin/network/xyo/sdkcorekotlin/node/interaction/XyoStandardInteractionTest.kt).

### Adding Custom Data to a Bound Witness

```kotlin
node.addHeuristic("MyHeuristic", object : XyoHeuristicGetter {
	// will get called right before the bound witness stares
	override fun getHeuristic(): XyoBuff? {
	    if (conditionIsMet()) {
	    	// object will be put into the bound witness
		return getMyHeuristic()
	    }

	    // object will not be put into the bound witness 
	    return null
	}
})
```

### Adding a Listener to a Node

```kotlin
node.addListener("MyListener", object : XyoNodeListener {
	override fun onBoundWitnessDiscovered(boundWitness: XyoBoundWitness) {
		// will get called when a new bound witness if found
	}

	override fun onBoundWitnessEndFailure(error: Exception?) {
		// will get called when a bound witness errors out
	}

	override fun onBoundWitnessEndSuccess(boundWitness: XyoBoundWitness) {
		// will get called when a bound witness is completed
	}

	override fun onBoundWitnessStart() {
		// will get called when a bound witness starts
	} 
})
```

### sdk-core-swift

[![Maintainability](https://api.codeclimate.com/v1/badges/587ae96e86057b6b6178/maintainability)](https://codeclimate.com/repos/5c4a7a7372b7b2029d008b34/maintainability) [![](https://img.shields.io/cocoapods/v/sdk-core-swift.svg?style=flat)](https://cocoapods.org/pods/sdk-core-swift) [![Test Coverage](https://api.codeclimate.com/v1/badges/587ae96e86057b6b6178/test_coverage)](https://codeclimate.com/repos/5c4a7a7372b7b2029d008b34/test_coverage)

[![Build Status](https://travis-ci.org/XYOracleNetwork/sdk-core-swift.svg?branch=master)](https://travis-ci.org/XYOracleNetwork/sdk-core-swift) 

A library to preform all core XYO Network functions.
This includes creating an origin chain, maintaining an origin chain, negotiations for talking to other nodes, and other basic functionality.
The library has heavily abstracted modules so that all operations will work with any crypto, storage, networking, ect.

The XYO protocol for creating origin-blocks is specified in the [XYO Yellow Paper](https://docs.xyo.network/XYO-Yellow-Paper.pdf). In it, it describes the behavior of how a node on the XYO network should create Bound Witnesses. Note, the behavior is not coupled with any particular technology constraints around transport layers, cryptographic algorithms, or hashing algorithms.

[Here](https://github.com/XYOracleNetwork/spec-coreobjectmodel-tex) is a link to the core object model that contains an index of major/minor values and their respective objects.

## Getting Started

The most common interface to this library through creating an origin chain creator object. Through an origin chain creator object one can create and maintain an origin chain. 

```swift
// this object will be used to hash items whiten the node
let hasher = XyoSha256()

// this is used as a key value store to persist
let storage = XyoInMemoryStorage()

// this is used as a place to store all of the bound witnesses/origin blocks
let chainRepo = XyoStorageOriginBlockRepository(storage: storage, hasher: hasher)

// this is used to save the state of the node (keys, index, previous hash)
let stateRepo = XyoStorageOriginChainStateRepository(storage: storage)

// this simply holds the state and the chain repository together
let configuration = XyoRepositoryConfiguration(originState: stateRepo, originBlock: chainRepo)

// the node to interface with creating an origin chain
let node = XyoOriginChainCreator(hasher: hasher, repositoryConfiguration: configuration)
```

After creating a node, it is standard to add a signer, and create a genesis block.

```swift
// creates a signer with a random private key
let signer = XyoSecp256k1Signer()
    
// adds the signer to the node
node.originState.addSigner(signer: signer)

// creates a origin block with its self (genesis block if this is the first block you make)
try node.selfSignOriginChain()
```

After creating a genesis block, your origin chain has officially started. Remember, all of the state is stored in the state repository (`XyoOriginChainStateRepository`) and the block repository (`XyoOriginBlockRepository`) that are constructed with the node. Both repositories are very high level and can be implemented for ones needs. Out of the box, this library comes with an implementation for key value store databases (`XyoStorageOriginBlockRepository`) and (`XyoStorageOriginChainStateRepository`). The `XyoStorageProvider` interface defines the methods for a simple key value store. There is a default implementation of an in memory key value store that comes with this library (`XyoInMemoryStorage`).

### Creating Origin Blocks

After a node has been created, it can be used to create origin blocks with other nodes. The process of talking to other nodes has been abstracted through use of a pipe (e.g. tcp, ble, memory) that handles all of the transport logic. This interface is defined as `XyoNetworkPipe`. This library ships with a memory pipe, and a tcp pipe.

**Using a tcp pipe** 

```swift
 // this defines who to create a tcp pipe with
let tcpPeer = XyoTcpPeer(ip: "myarchivist.com", port: 11000)

// prepares a socket tcp to communicate with the other node
let socket = XyoTcpSocket.create(peer: tcpPeer)

// wraps the socket to comply to the pipe interface
let pipe = XyoTcpSocketPipe(socket: socket, initiationData: nil)

// wraps the pipe to preform standard communications
let handler = XyoNetworkHandler(pipe: pipe)

node.boundWitness(handler: handler, procedureCatalogue: XyoProcedureCatalogue) { (boundWitness, error) in
    
}
```

**Using a memory pipe** 

```swift
let pipeOne = XyoMemoryPipe()
let pipeTwo = XyoMemoryPipe()

pipeOne.other = pipeTwo
pipeTwo.other = pipeOne

let handlerOne = XyoNetworkHandler(pipe: pipeOne)
let handlerTwo = XyoNetworkHandler(pipe: pipeTwo)

nodeOne.boundWitness(handler: handlerOne, procedureCatalogue: TestInteractionCatalogueCaseOne()) { (result, error) in
    // this should complete first
}

nodeTwo.boundWitness(handler: handlerTwo, procedureCatalogue: TestInteractionCatalogueCaseOne()) { (result, error) in
    // this should complete second
}
```

  More example and bridge interactions can be found [here](https://github.com/XYOracleNetwork/sdk-core-swift/tree/docs/sdk-core-swiftTests/node/interaction)

 **Bluetooth**

 Bluetooth swift pipes for client and server can be found [here](https://github.com/XYOracleNetwork/sdk-xyobleinterface-swift).

 **Other**

 Other network pipes can be implemented as long as the follow the interface defined [here](https://github.com/XYOracleNetwork/sdk-core-swift/blob/docs/sdk-core-swift/network/XyoNetworkPipe.swift).

### Adding custom data to bound witnesses.

 To add custum data to a bound witnesses, a XyoHueresticGetter can be created:

```swift
public struct MyCustomData: XyoHueresticGetter {
   public func getHeuristic() -> XyoObjectStructure? {
       if (conditionIsMet) {
           let myData = getDataSomehow()
           return myData
       }
       
       return nil
   }
}
```

 After the getter has been created, it can be added to a node by calling:

```swift
let myDataForBoundWitness = MyCustomData()
node.addHuerestic (key: "MyData", getter : myDataForBoundWitness)
```

### Adding a listener to a node

```swift
 struct MyListener : XyoNodeListener {
    /// This function will be called every time a bound witness has started
    func onBoundWitnessStart() {
        // update UI
    }
    
    /// This function is called when a bound witness starts, but fails due to an error
    func onBoundWitnessEndFailure() {
        // update UI
    }
    
    /// This function is called when the node discovers a new origin block, this is typicaly its new blocks
    /// that it is creating, but will be called when a bridge discovers new blocks.
    /// - Parameter boundWitness: The boundwitness just discovered
    func onBoundWitnessDiscovered(boundWitness : XyoBoundWitness) {
     // update UI
    }
    
    /// This function is called every time a bound witness starts and complets successfully.
    /// - Parameter boundWitness: The boundwitness just completed
    func onBoundWitnessEndSuccess(boundWitness : XyoBoundWitness) {
        // update UI
    }
}
```

  You may add a listener to a node by adding the following:

```swift
let listener = MyListener()
myNode.addListener(key: "MyListener", listener : listener)
```

## TCP Node

The following code is an example of a node that bound witnesses with a server 10 times.

```swift
let storage = XyoInMemoryStorage()
let blocks = XyoStrageProviderOriginBlockRepository(storageProvider: storage,
                                                    hasher: XyoSha256())
let state = XyoStorageOriginChainStateRepository(storage: storage)
let conf = XyoRepositoryConfiguration(originState: state, originBlock: blocks)
let node = XyoRelayNode(hasher: XyoSha256(),
                        repositoryConfiguration: conf,
                        queueRepository: XyoStorageBridgeQueueRepository(storage: storage))

node.originState.addSigner(signer: XyoSecp256k1Signer())

for i in 0..9 {
    let peer = XyoTcpPeer(ip: "alpha-peers.xyo.network", port: 11000)
    let socket = XyoTcpSocket.create(peer: peer)
    let pipe = XyoTcpSocketPipe(socket: socket, initiationData: nil)
    let handler = XyoNetworkHandler(pipe: pipe)

    let data = UInt32(XyoProcedureCatalogueFlags.TAKE_ORIGIN_CHAIN | XyoProcedureCatalogueFlags.GIVE_ORIGIN_CHAIN)
    node.boundWitness(handler: handler, procedureCatalogue: XyoFlagProcedureCatalogue(forOther: data, withOther: data)) { (result, error) in

    }
}
```

> There are differences in some implementations, but both libraries share origin chain and block creation

### Examples of shared functions

XY2BluetoothDevice

-   `find()`

XY3BluetoothDevice

-   `find()`
-   `stayAwake()`
-   `fallAsleep()`
-   `lock()`
-   `unlock()`

XY4BluetoothDevice

-   `lock()`
-   `unlock()`
-   `stayAwake()`
-   `fallAsleep()`
-   `find()`

XYGpsBluetoothDevice

-   `find()`
-   `stayAwake()`

Shared functions to be renamed 

`addService`

Swift 

-   `XYCBPeripheralManager.swift`

Android 

-   `XyBluetoothGattServer.kt`

`removeService`

Swift 

-   `XYCBPeripheralManager.swift`

Android 

-   `XYBluetoothGattServer.kt`

`startAdvertising`

Swift 

-   `XYCBPeripheralManager.swift`

Android 

-   `XYBluetoothAdvertiser.kt`

`stopAdvertising`

Swift 

-   `XYCBPeripheralManager.swift`

Android 

-   `XYBluetoothAdvertiser.kt`

`addCharacteristic`

Swift 

-   `XYMutableService.swift`

Android 

-   `XYOServerActivity.kt`

### Shared Properties Files with some shared enumerators

-   `DeviceInformationService`

-   `GenericAccessService`

-   `GenericAttributeService`

-   `LinkLossService`

-   `TxPowerService`

-   XY3 - `BasicConfigService`

-   XY3 - `ControlService`

-   XY3 - `ExtendedConfigService`

-   XY3 - `ExtendedControlService`

-   XY4 - `PrimaryService` (In Swift it’s `XyFinderPrimaryService`)

-   `XYSmartScan`
