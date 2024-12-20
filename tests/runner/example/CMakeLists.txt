# Copyright (c) 2024 Basalte bv
# SPDX-License-Identifier: Apache-2.0

cmake_minimum_required(VERSION 3.20.0)
find_package(Zephyr REQUIRED HINTS $ENV{ZEPHYR_BASE})
project(app_example_runner_test)

target_sources(app PRIVATE ${ZEPHYR_BASE}/misc/empty_file.c)

include(west)

enable_testing()
include(CTest)

add_test(
  NAME example-runner
  COMMAND ${WEST} simulate --runner example
)
set_property(
  TEST example-runner
  PROPERTY PASS_REGULAR_EXPRESSION "Running simulate on ${CONFIG_BOARD}"
)
