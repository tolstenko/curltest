cmake_minimum_required(VERSION 3.9)

set(CMAKE_CXX_STANDARD 11)

include(cmake/HunterGate.cmake)

HunterGate(
    URL "https://github.com/ruslo/hunter/archive/v0.20.63.tar.gz"
    SHA1 "358385a57457e5276f9e9db6e8e2bc80c53287ad"
)

project(curltest)

hunter_add_package(curl)
find_package(curl CONFIG REQUIRED)

add_executable(curltest main.cpp)
IF(MINGW)
  target_link_libraries(curltest PUBLIC CURL::libcurl wsock32 ws2_32)
ELSE()
  target_link_libraries(curltest PUBLIC CURL::libcurl)
ENDIF()