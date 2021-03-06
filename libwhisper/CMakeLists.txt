set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -DSTATICLIB")

aux_source_directory(. SRC_LIST)

file(GLOB HEADERS "*.h")

add_library(whisper ${SRC_LIST} ${HEADERS})

find_package(Dev)

target_include_directories(whisper PRIVATE ..)
target_include_directories(whisper PRIVATE ../utils)
target_include_directories(whisper PUBLIC ${BOOST_INCLUDE_DIR})
include_directories(../libodbc/include
					../libodbc/include/db2_linux
					../libodbc/include/ibase
					../libodbc/include/infomix
					../libodbc/include/mysql
					../libodbc/include/odbc_linux
					../libodbc/include/pgsql
					../libodbc/include/sqlbase
					../libodbc/include/sqllite
					../libodbc/include/ss_linux
					../libodbc/include/sybase)

target_link_libraries(whisper Boost::Regex)
target_link_libraries(whisper ${Dev_DEVCORE_LIBRARIES})
target_link_libraries(whisper ${Dev_DEVCRYPTO_LIBRARIES})
target_link_libraries(whisper ${Dev_P2P_LIBRARIES})

install(TARGETS whisper RUNTIME DESTINATION bin ARCHIVE DESTINATION lib LIBRARY DESTINATION lib)
