find_package(Jwt CONFIG QUIET)

if(Jwt_FOUND)
  #get_property(_loc TARGET Jwt::jwt PROPERTY LOCATION)
  #message(STATUS "Found Jwt: ${_loc} (found version ${Jwt_VERSION})")
  #add_library(Jwt_external INTERFACE)
else()
  include(ExternalProject)
  ExternalProject_Add(Jwt_external
    URL
     https://github.com/pokowaka/jwt-cpp/archive/v1.1.zip
    CMAKE_ARGS
	  #-DOPENSSL_INCLUDE_DIRS=/C/msys64/mingw32/include #
	  #-DOPENSSL_LIBRARY_DIRS=/C/msys64/mingw32/lib	    #
	  -DOPENSSL_INCLUDE_DIRS=/C/OpenSSL-Win32/include
	  -DOPENSSL_LIBRARY_DIRS=/C/OpenSSL-Win32/lib
	  -DOPENSSL_LIBRARIES=libcrypto;libssl
      -DCMAKE_INSTALL_PREFIX=${STAGED_INSTALL_PREFIX}
      -DENABLE_TESTS=OFF
	  -DBUILD_SHARED_LIBS=ON
    )
	
  include(GNUInstallDirs)

  set(
    Jwt_DIR ${STAGED_INSTALL_PREFIX}/${CMAKE_INSTALL_LIBDIR}/cmake/Jwt
    CACHE PATH "Path to internally built Jwt_Config.cmake"
    FORCE
    )
	
endif()


