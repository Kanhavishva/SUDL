PROJECT(proto)
CMAKE_MINIMUM_REQUIRED(VERSION 2.6)
FIND_PACKAGE(Protobuf REQUIRED)

if(EXISTS ${PROTOBUF_PROTOC_EXECUTABLE})
    message(STATUS "Found PROTOBUF Compiler: ${PROTOBUF_PROTOC_EXECUTABLE}")
else()
    message(FATAL_ERROR "Could not find PROTOBUF Compiler")
endif()

PROTOBUF_GENERATE_CPP(PROTO_SRCS PROTO_HDRS sudl.proto)
add_library(proto ${PROTO_SRCS} ${PROTO_HDRS})
target_link_libraries(proto ${PROTOBUF_LIBRARIES} pthread)


AUX_SOURCE_DIRECTORY(. GR_S)
ADD_EXECUTABLE(su ${GR_S})
TARGET_LINK_LIBRARIES(su proto)
