# CMake 最低版本号要求
cmake_minimum_required (VERSION 3.0)

# 项目信息
project (HelloWorld)

add_compile_options(-std=c++11)
# add_definitions(-DIOS_64 -DIOS_LINUX)

# 查找当前目录下的所有源文件
# 并将名称保存到 DIR_SRCS 变量
aux_source_directory(. DIR_SRCS)

# include_directories(../../../../../ThirdPartyLib/opencv-3.1.0/include/)


# 在CMakeLists中 link_directories 是编译时要找的路径，也是运行时要找的路径。。。
# 并且是相对了makefile的路径,而不是MakeLists(2.18)
# 并且是相对了MakeLists(3.2)
# opencv
# link_directories(../../../../../ThirdPartyLib/opencv-3.1.0/build/lib)
# tinyxml2
# link_directories(../../../../../ThirdPartyLib/tinyxml2-2.1.0/)

# jsoncpp
# link_directories(../../../../../ThirdPartyLib/jsoncpp/)

# EwaySys
# link_directories(../../../Bin/Debug/)

#　sdk
# link_directories(/usr/share/ewaybot/lib)
# link_directories(/usr/share/ewaybot/thirdpartylib)




# 指定生成目标
add_executable(HelloWorld   
	Solution.cpp
	main.cpp)

# 指定链接库
# target_link_libraries(MATLABFunction 
# 	jsoncpp
# 	tinyxml2
# 	opencv_core
# 	opencv_imgproc	
# 	opencv_videoio
# 	opencv_highgui
# 	EwaySys)

# 意思为在安装时要加上这些rpath　(INSTALL_RPATH)
# 这一句必须是在　install 之前 add_library之后否则会提示MATLABFunction找不到
#SET_TARGET_PROPERTIES(MATLABFunction
    #PROPERTIES INSTALL_RPATH "$ORIGIN/../../../../../../ThirdPartyLib/tinyxml2-2.1.0/:$ORIGIN/../../../../../../ThirdPartyLib/jsoncpp/:$ORIGIN/../../../../../../ThirdPartyLib/opencv-3.1.0/include/:/usr/share/ewaybot/lib:/usr/share/ewaybot/thirdpartylib")

# VERSION指代动态库版本，SOVERSION指代API版本
#SET_TARGET_PROPERTIES(MATLABFunction PROPERTIES VERSION 1.0.0 SOVERSION 1)

# 设置安装路径，说白了，库拷到哪里，这里有设置相对路径的方法
#install(TARGETS MATLABFunction DESTINATION ${CMAKE_CURRENT_SOURCE_DIR}/../../Bin/Debug/MATLABFunction)


#　通用的方法是在install之后(前提是install路径不能是makefile当前是的路径)，cmake会将所有的rpath消除掉
#　清除掉之后，如果想用这个库的话，再设置LD_LIBRARY_PATH　让这个库能正确的找到相应的链接库，这是linux常用通用的办法　
# ros,gazebo,v-rep尽是如此　
# 但是Ewayos里的库不想采用这种方法，要加origin　path来解决这个问题，于是产生了SET_TARGET_PROPERTIES　这种方法　






