cmake_minimum_required(VERSION 3.20)

project(rpi-cloud-pong)

set(CMAKE_CXX_STANDARD 17)

include(FetchContent)

FetchContent_Declare(
    SigFn
    GIT_REPOSITORY https://github.com/maxtek6/sigfn.git
    GIT_TAG        master
)
FetchContent_MakeAvailable(SigFn)