
find_package(Protobuf)

if(PROTOBUF_FOUND)
    protobuf_generate_cpp(CAFFE_PROTO_SRCS CAFFE_PROTO_HDRS caffe.proto)
    add_executable(caffe2ncnn caffe2ncnn.cpp ${CAFFE_PROTO_SRCS} ${CAFFE_PROTO_HDRS})
    target_include_directories(caffe2ncnn
        PRIVATE
            ${PROTOBUF_INCLUDE_DIR}
            ${CMAKE_CURRENT_BINARY_DIR})
    target_compile_features(caffe2ncnn PRIVATE cxx_std_11)
    target_link_libraries(caffe2ncnn PRIVATE ${PROTOBUF_LIBRARIES})
else()
    message(WARNING "Protobuf not found, caffe model convert tool won't be built")
endif()
