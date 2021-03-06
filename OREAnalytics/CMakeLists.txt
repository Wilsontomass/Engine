cmake_minimum_required(VERSION 3.8)

project(OREAnalytics CXX)

enable_testing()

include("../cmake/writeAll.cmake")
include("../cmake/writeTestSuiteMain.cmake")
include("../cmake/commonSettings.cmake")

get_library_name("OREAnalytics" OREA_LIB_NAME)
get_library_name("OREData" ORED_LIB_NAME)
get_library_name("QuantExt" QLE_LIB_NAME)
get_library_name("QuantLib" QL_LIB_NAME)
configure_msvc_runtime()

find_package (Boost REQUIRED COMPONENTS unit_test_framework regex date_time serialization filesystem timer OPTIONAL_COMPONENTS chrono)

include_directories(${Boost_INCLUDE_DIRS})
include_directories(${QUANTLIB_SOURCE_DIR})
include_directories(${QUANTEXT_SOURCE_DIR})
include_directories(${OREDATA_SOURCE_DIR})
include_directories(${ORETEST_SOURCE_DIR})
include_directories(${RAPIDXML_SOURCE_DIR})
include_directories(${CMAKE_CURRENT_SOURCE_DIR})

add_link_directory_if_exists("${QUANTLIB_SOURCE_DIR}/build/ql")
add_link_directory_if_exists("${QUANTEXT_SOURCE_DIR}/build/qle")
add_link_directory_if_exists("${OREDATA_SOURCE_DIR}/build/ored")

add_subdirectory("orea")
add_subdirectory("doc")
add_subdirectory("test")
