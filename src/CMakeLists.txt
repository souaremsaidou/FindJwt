cmake_minimum_required(VERSION 3.5 FATAL_ERROR)

project(recipe-02_core LANGUAGES CXX)

find_package(Jwt CONFIG REQUIRED)

add_executable(claim_validator claim_validator.cpp)

target_link_libraries(claim_validator
  PUBLIC
    Jwt::jwt
  )