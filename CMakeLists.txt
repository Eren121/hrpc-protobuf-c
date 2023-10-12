project(hrpc-protobuf-c
	VERSION 1.0
	LANGUAGES CXX C
)

set(TMP_DIR ${PROJECT_BINARY_DIR}/protoc-generated)
file(MAKE_DIRECTORY ${TMP_DIR}/protobuf-c)
generate_protoc_cpp_source(
	${TMP_DIR}/protobuf-c
	${PROJECT_SOURCE_DIR}/protobuf-c/
	protobuf-c.proto
)

add_library(
	hrpc-protobuf-c
	protobuf-c/protobuf-c.c
	protobuf-c/protobuf-c.h
	${TMP_DIR}/protobuf-c/protobuf-c.pb.cc
	${TMP_DIR}/protobuf-c/protobuf-c.pb.h
)

target_include_directories(hrpc-protobuf-c PUBLIC ${PROJECT_SOURCE_DIR})
target_include_directories(hrpc-protobuf-c PUBLIC ${PROJECT_SOURCE_DIR}/protobuf-c)
target_link_libraries(hrpc-protobuf-c PUBLIC protobuf::libprotoc libprotobuf)

add_executable(
	hrpc-protobuf-c-plugin
	protoc-c/c_bytes_field.cc
	protoc-c/c_bytes_field.h
	protoc-c/c_enum.cc
	protoc-c/c_enum.h
	protoc-c/c_enum_field.cc
	protoc-c/c_enum_field.h
	protoc-c/c_extension.cc
	protoc-c/c_extension.h
	protoc-c/c_field.cc
	protoc-c/c_field.h
	protoc-c/c_file.cc
	protoc-c/c_file.h
	protoc-c/c_generator.cc
	protoc-c/c_generator.h
	protoc-c/c_helpers.cc
	protoc-c/c_helpers.h
	protoc-c/c_message.cc
	protoc-c/c_message.h
	protoc-c/c_message_field.cc
	protoc-c/c_message_field.h
	protoc-c/c_primitive_field.cc
	protoc-c/c_primitive_field.h
	protoc-c/c_service.cc
	protoc-c/c_service.h
	protoc-c/c_string_field.cc
	protoc-c/c_string_field.h
	protoc-c/main.cc
)

target_link_libraries(hrpc-protobuf-c-plugin PUBLIC hrpc-protobuf-c)
target_include_directories(hrpc-protobuf-c-plugin PUBLIC ${TMP_DIR})