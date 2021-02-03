cmake_minimum_required(VERSION 2.6)

set(AMO_NAME usb-amo)

project(${AMO_NAME})

find_package(PkgConfig REQUIRED)
#find_package(CURL REQUIRED)
#find_package(ZLIB REQUIRED)
pkg_check_modules(coreusp coreusp REQUIRED)
#pkg_check_modules(ARES libcares REQUIRED)
#pkg_check_modules(SQL REQUIRED sqlite3)
#pkg_check_modules(MOSQUITTOPP REQUIRED libmosquittopp)
#pkg_check_modules(MOSQUITTO REQUIRED libmosquitto)
#include_directories(${CURL_INCLUDE_DIR})
#include_directories(${ZLIB_INCLUDE_DIR})
#include_directories(${CMAKE_CURRENT_SOURCE_DIR}/src/protobuf-c/)
#include_directories(${CMAKE_CURRENT_SOURCE_DIR}/src/vendor/)
#include_directories(${CMAKE_CURRENT_SOURCE_DIR}/src/include/)
#include_directories(${CMAKE_CURRENT_SOURCE_DIR}/src/libjson/ccan/json/)

SET(TARGET_SRC
    main.c
    )
set(CMAKE_C_FLAGS "${CMAKE_C_FLAGS} -Werror -Werror=unused-value -Werror=format -Winit-self -Wparentheses -Werror=parentheses -Wuninitialized -Werror=uninitialized -Wpointer-arith")
link_directories(${CMAKE_CURRENT_BINARY_DIR})
SET(CMAKE_EXE_LINKER_FLAGS
          "${CMAKE_EXE_LINKER_FLAGS} -Wl,-rpath -Wl,$ORIGIN")
      
ADD_LIBRARY (${AMO_NAME} SHARED ${TARGET_SRC})

#target_link_libraries(${AMO_NAME} ${SQL_LIBRARIES} ${MOSQUITTO_LIBRARIES} ${MOSQUITTOPP_LIBRARIES} ${ZLIB_LIBRARIES} ${CURL_LIBRARIES} ${SQLITE3_LIBRARIES} ${ARES_LIBRARIES} ${OpenSSL_LIBRARIES} -lm -ldl -lpthread -lrt  -l${AMO_NAME})
#set_target_properties(${AMO_NAME} PROPERTIES PUBLIC_HEADER "src/include/usp_api.h;src/include/usp_err_codes.h;src/include/vendor_api.h")

install(TARGETS ${AMO_NAME} 
    LIBRARY DESTINATION lib/amo
    PUBLIC_HEADER DESTINATION include)
