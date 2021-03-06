cmake_minimum_required(VERSION 2.6)
project(twiccards)

if (WIN32)
	SET(VERSION_PRODUCTNAME_VALUE "twiccards")
	add_definitions(-DVERSION_PRODUCTNAME_VALUE="${VERSION_PRODUCTNAME_VALUE}")
endif()

file(GLOB_RECURSE SRCS *.cpp)
file(GLOB_RECURSE INCLUDE *.hpp)

add_library(
	twiccards
	SHARED
	${SRCS}
	${INCLUDE}
	${resourcerc}
  )

SET_TARGET_PROPERTIES(twiccards PROPERTIES VERSION ${LIBLOGICALACCESS_VERSION_STRING})
  
target_link_libraries(
	twiccards
	iso7816cards
	${LIBLOGICALACCESS_LIBRARY}
)

install ( FILES ${INCLUDE} DESTINATION include/logicalaccess/plugins/cards/twic )
install ( TARGETS twiccards RUNTIME DESTINATION bin/${LIB_SUFFIX} ARCHIVE DESTINATION lib/${LIB_SUFFIX} LIBRARY DESTINATION lib/${LIB_SUFFIX} )