AUX_SOURCE_DIRECTORY(. TEST_SOURCES)
INCLUDE_DIRECTORIES(
  ${PROXY_SOURCE_DIR}/contrib/googletest
  ${PROXY_SOURCE_DIR}/contrib/googletest/include
  ${PROXY_SOURCE_DIR}/src
)

FOREACH(SRC ${TEST_SOURCES})
  STRING(REGEX REPLACE ".*/(.*)\\.cpp$" "\\1" TGT ${SRC})
  ADD_EXECUTABLE(
    ${TGT} ${SRC}
    ${PROXY_SOURCE_DIR}/contrib/googletest/src/gtest-all.cc
    ${PROXY_SOURCE_DIR}/contrib/googletest/src/gtest_main.cc
  )
  TARGET_LINK_LIBRARIES(${TGT}
    ${CAF_LIBRARIES}
    ${Boost_LIBRARIES}
    ${ZLIB_LIBRARIES}
    ${OPENSSL_CRYPTO_LIBRARY}
    pthread
  )
  ADD_TEST(NAME ${TGT} COMMAND ${TGT})
ENDFOREACH()
