CMAKE_MINIMUM_REQUIRED( VERSION 2.8 ) #设定版本
PROJECT( karto ) #设定工程名
SET( CMAKE_CXX_COMPILER "g++") #设定编译器
SET( CMAKE_BUILD_TYPE Release  )
SET( CMAKE_CXX_FLAGS "-std=c++11 -O3")
	
#设定可执行二进制文件的目录
SET( EXECUTABLE_OUTPUT_PATH ${PROJECT_SOURCE_DIR}/build)
	
#设定头文件目录
INCLUDE_DIRECTORIES( ${PROJECT_SOURCE_DIR}/include)
	
# 增加opencv的依赖
FIND_PACKAGE( OpenCV REQUIRED )
INCLUDE_DIRECTORIES( ${OpenCV_INCLUDE_DIRS} )
message(${OpenCV_INCLUDE_DIRS})

# 增加Boost
FIND_PACKAGE( Boost REQUIRED )
INCLUDE_DIRECTORIES( ${Boost_INCLUDE_DIRS} )
message(${Boost_INCLUDE_DIRS})

#FIND_PACKAGE( Eigen3 REQUIRED )
INCLUDE_DIRECTORIES( /usr/include/eigen3 )

# 添加g2o的依赖
# 因为g2o不是常用库，要添加它的findg2o.cmake文件
LIST( APPEND CMAKE_MODULE_PATH ${PROJECT_SOURCE_DIR}/cmake_modules )
SET( G2O_ROOT /usr/local/include/g2o )
FIND_PACKAGE( G2O REQUIRED )
# CSparse
FIND_PACKAGE( CSparse REQUIRED )
INCLUDE_DIRECTORIES( ${G2O_INCLUDE_DIR} ${CSPARSE_INCLUDE_DIR} )
message(${G2O_INCLUDE_DIR})
message(${CSPARSE_INCLUDE_DIR})

#ADD_EXECUTABLE( main main.cpp Karto.cpp Mapper.cpp g2o_solver.cpp )
#TARGET_LINK_LIBRARIES( main ${OpenCV_LIBRARIES} ${Boost_LIBRARIES} boost_system boost_filesystem pthread boost_thread g2o_stuff g2o_core g2o_types_slam2d g2o_solver_csparse g2o_csparse_extension ext_csparse ${CSPARSE_LIBRARY} )

ADD_EXECUTABLE( main main.cpp Karto.cpp Mapper.cpp g2o_solver.cpp )
TARGET_LINK_LIBRARIES( main ${OpenCV_LIBRARIES} ${Boost_LIBRARIES} boost_system boost_filesystem pthread boost_thread g2o_stuff g2o_core g2o_types_slam2d g2o_solver_csparse g2o_csparse_extension  ${CSPARSE_LIBRARY} )

