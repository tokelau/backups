include(FetchContent)
FetchContent_Declare(gtest
  QUIET
  URL https://github.com/google/googletest/archive/release-1.10.0.tar.gz
)
# configure build of googletest
set(gtest_force_shared_crt ON CACHE BOOL "" FORCE)
set(BUILD_GMOCK OFF CACHE BOOL "" FORCE)
FetchContent_MakeAvailable(gtest)

#FetchContent_Declare(zstd
#        QUIET
#        URL https://github.com/facebook/zstd/releases/download/v1.5.2/zstd-1.5.2.tar.gz
#        )
#FetchContent_MakeAvailable(zstd)

FetchContent_Declare(libzip
        QUIET
        URL https://libzip.org/download/libzip-1.8.0.tar.xz
        )
set(ENABLE_ZSTD "Enable use of Zstandard" ON)

FetchContent_MakeAvailable(libzip)

FetchContent_Declare(libzippp
        QUIET
        URL https://github.com/ctabin/libzippp/archive/refs/tags/libzippp-v5.0-1.8.0.tar.gz
        )
FetchContent_MakeAvailable(libzippp)

add_executable(
    unit_tests
        lab3_tests.cpp
)

target_link_libraries(unit_tests
  PRIVATE
    labs
    gtest_main
  )

# automatic discovery of unit tests
include(GoogleTest)
gtest_discover_tests(unit_tests
  PROPERTIES
    LABELS "unit"
  DISCOVERY_TIMEOUT  # how long to wait (in seconds) before crashing
    240
  )
