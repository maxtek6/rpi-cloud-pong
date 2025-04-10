# rpi-cloud-pong
Raspberry Pi Cloud Pong project for cloud-based pong game.
At a high-level, client will handle joystick events from player and then serialize the game input and send over to the server.
Server will compute updated game state for a session and send updated game state back to clients via a flatbuffer that will be deserialized by clients.
Server will be able to handle multiple gaming sessions with either computer or two human players against each other.

## Prerequisites

Make sure you have the following installed:

cmake
g++

## Instructions for proper cloning of project
Note: It is highly recommended to clone with the following option so that required submodules are clone as well:
Note: This project has been validated with the specific version of flatbuffers shown below, hence why it is pulled and built from source, as this version is not readibly available from install.
```bash
git clone --recurse-submodule https://github.com/maxtek6/rpi-cloud-pong.git
cd rpi-cloud-pong/flatbuffers
git checkout v24.3.25
```

## Prereq: Building flatc and generating header from schema
1. Build flatbuffer from source (currently need to explictly build this version from source and run the built flatc compiler)
```bash
# Go to flatbuffers source directory, build flatc compiler from source and generate header file
cd <root-of-rpi-cloud-pong>
cd flatbuffers
cmake -B build -DCMAKE_INSTALL_PREFIX=../flatbuffers/install
cmake --build build -j
cmake --install build
./install/bin/flatc --cpp -o ../generated ../schema/pongdata.fbs

# Now Rpi pong server and client will have requried pong header file in generated folder.
```

## Building Server
```bash
cd <root-of-rpi-cloud-pong>
cd rpi-pong-server
mkdir build
cd build
cmake ..
make -j
```

## Building Client
```bash
cd <root-of-rpi-cloud-pong>
cd rpi-pong-client
mkdir build
cd build
cmake ..
make -j
```

## Running Programs (recommended to be ran in the following order)
## 1. Run Client
```bash
cd <root-of-rpi-cloud-pong>
cd rpi-pong-server
./build/rpi-pong-server
```

## 2. Run Server
## NOTE: A connected joystick to the machine running client is required!!
```bash
cd <root-of-rpi-cloud-pong>
cd rpi-pong-client
./build/rpi-pong-client
```
