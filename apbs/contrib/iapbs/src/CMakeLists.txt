
#SET(APBS_AUX_PATH ${APBS_SRC_PATH}/src/CMakeFiles/apbs.dir)

INCLUDE_DIRECTORIES(. ${APBS_ROOT}/src ${APBS_INST_PATH}/include)
LINK_DIRECTORIES(${APBS_ROOT_PATH}/lib)

#ADD_LIBRARY(iapbs SHARED apbs_driver.c apbs_driver.h)
ADD_LIBRARY(iapbs STATIC apbs_driver.c apbs_driver.h)

option(BUILD_WRAPPER "Optionally build Fortran wrapper" OFF)
if(BUILD_WRAPPER)
   ENABLE_LANGUAGE(Fortran)
   ADD_EXECUTABLE(wrapper wrapper.f)
   TARGET_LINK_LIBRARIES(wrapper 
     iapbs
     apbs_routines
     apbs_mg
     apbs_generic
     apbs_pmgc)
   INSTALL(TARGETS wrapper DESTINATION bin)
endif()

INSTALL(TARGETS iapbs DESTINATION lib)

install(FILES apbs_driver.h DESTINATION include/iapbs)
