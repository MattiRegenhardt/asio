cmake_minimum_required(VERSION 3.18)
project(asio CXX)

option(ASIO_DISABLE_EXCEPTIONS "Disable ASIO exceptions" ON)

add_library(
        asio
        INTERFACE
)
target_compile_features(
        asio
        INTERFACE

        cxx_std_11
)
target_compile_definitions(
        asio
        INTERFACE

        $<$<BOOL:${ASIO_DISABLE_EXCEPTIONS}>:ASIO_DISABLE_STD_EXCEPTION_PTR=1>
        $<$<BOOL:${ASIO_DISABLE_EXCEPTIONS}>:ASIO_DISABLE_STD_NESTED_EXCEPTION=1>
        $<$<BOOL:${ASIO_DISABLE_EXCEPTIONS}>:ASIO_NO_EXCEPTIONS=1>
)
target_include_directories(
        asio
        INTERFACE

        $<BUILD_INTERFACE:${CMAKE_CURRENT_SOURCE_DIR}/asio/asio/include>
        $<INSTALL_INTERFACE:include>
)
add_library(asio::asio ALIAS asio)
