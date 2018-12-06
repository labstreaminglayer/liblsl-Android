# Sets the minimum version of CMake required to build the native
# library. You should either keep the default value or only pass a
# value of 3.4.0 or lower.

cmake_minimum_required(VERSION 3.4.1)

# Creates and names a library, sets it as either STATIC
# or SHARED, and provides the relative paths to its source code.
# You can define multiple libraries, and CMake builds it for you.
# Gradle automatically packages shared libraries with your APK.

add_library( # Sets the name of the library.
             lsl

             # Sets the library as a shared library.
             SHARED

             # Provides a relative path to your source file(s).
             # Associated headers in the same location as their source
             # file are automatically included.
	"../../liblsl/src/api_config.cpp"
	"../../liblsl/src/common.cpp"
	"../../liblsl/src/consumer_queue.cpp"
	"../../liblsl/src/data_receiver.cpp"
	"../../liblsl/src/info_receiver.cpp"
	"../../liblsl/src/inlet_connection.cpp"
	"../../liblsl/src/lsl_continuous_resolver_c.cpp"
	"../../liblsl/src/lsl_freefuncs_c.cpp"
	"../../liblsl/src/lsl_inlet_c.cpp"
	"../../liblsl/src/lsl_outlet_c.cpp"
	"../../liblsl/src/lsl_streaminfo_c.cpp"
	"../../liblsl/src/lsl_xml_element_c.cpp"
	"../../liblsl/src/pugixml/pugixml.cpp"
	"../../liblsl/src/resolver_impl.cpp"
	"../../liblsl/src/resolve_attempt_udp.cpp"
	"../../liblsl/src/sample.cpp"
	"../../liblsl/src/send_buffer.cpp"
	"../../liblsl/src/socket_utils.cpp"
	"../../liblsl/src/stream_info_impl.cpp"
	"../../liblsl/src/stream_outlet_impl.cpp"
	"../../liblsl/src/tcp_server.cpp"
	"../../liblsl/src/time_postprocessor.cpp"
	"../../liblsl/src/time_receiver.cpp"
	"../../liblsl/src/udp_server.cpp"
	"../../liblsl/lslboost/libs/thread/src/tss_null.cpp"
	"../../liblsl/lslboost/libs/system/src/error_code.cpp"
	"../../liblsl/lslboost/libs/chrono/src/chrono.cpp"
	"../../liblsl/lslboost/libs/serialization/src/archive_exception.cpp"
	"../../liblsl/lslboost/libs/serialization/src/basic_archive.cpp"
	"../../liblsl/lslboost/libs/serialization/src/basic_iarchive.cpp"
	"../../liblsl/lslboost/libs/serialization/src/basic_iserializer.cpp"
	"../../liblsl/lslboost/libs/serialization/src/basic_oarchive.cpp"
	"../../liblsl/lslboost/libs/serialization/src/basic_oserializer.cpp"
	"../../liblsl/lslboost/libs/serialization/src/basic_serializer_map.cpp"
	"../../liblsl/lslboost/libs/serialization/src/extended_type_info.cpp"
	"../../liblsl/lslboost/libs/serialization/src/extended_type_info_typeid.cpp"
	"../../liblsl/lslboost/libs/serialization/src/void_cast.cpp"
	"../../liblsl/lslboost/libs/atomic/src/lockpool.cpp"
	"../../liblsl/lslboost/libs/program_options/src/convert.cpp"
	"../../liblsl/lslboost/libs/program_options/src/utf8_codecvt_facet.cpp"
	"../../liblsl/lslboost/libs/thread/src/pthread/once.cpp"
	"../../liblsl/lslboost/libs/thread/src/pthread/thread.cpp"
             )

target_include_directories(lsl PUBLIC ../../liblsl/lslboost)
target_compile_definitions(lsl PUBLIC
	BOOST_ASIO_ENABLE_OLD_SERVICES
	BOOST_ASIO_USE_BOOST_DATE_TIME_FOR_SOCKET_IOSTREAM
)

#use CMAKE_STATIC_LINKER_FLAGS for static library. Compiler flags are in build.gradle.
#set(CMAKE_SHARED_LINKER_FLAGS "-z muldefs")

# Searches for a specified prebuilt library and stores the path as a
# variable. Because system libraries are included in the search path by
# default, you only need to specify the name of the public NDK library
# you want to add. CMake verifies that the library exists before
# completing its build.

find_library( # Sets the name of the path variable.
              log-lib

              # Specifies the name of the NDK library that
              # you want CMake to locate.
              log )

# Specifies libraries CMake should link to your target library. You
# can link multiple libraries, such as libraries you define in the
# build script, prebuilt third-party libraries, or system libraries.

target_link_libraries( # Specifies the target library.
                       lsl

                       # Links the target library to the log library
                       # included in the NDK.
                       ${log-lib} )
					   
