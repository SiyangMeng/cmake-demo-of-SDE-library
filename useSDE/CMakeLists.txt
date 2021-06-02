cmake_minimum_required (VERSION 3.8)

project (getSDELibs)
# 设置.exe的文件名
set(EXE_NAME "testSDE02")
# 设置.dll的生成位置，默认是和bin相同
 set(LIBRARY_OUTPUT_PATH ${PROJECT_SOURCE_DIR}/lib)

# 查找src所有子文件夹里的.cpp文件
file(GLOB LIB_SRC
	"src/*.cpp"
	"src/models/*.cpp"
)

# # add_subdirectory(src)
# # find_library(SDE "libSDE.dll" PATHS "${PROJECT_SOURCE_DIR}/lib")

# 由于实在查找不到libSDE.dll，因此采用直接设定文件位置的方法
set(SDE "${PROJECT_SOURCE_DIR}/lib/libSDE.dll")

# 编译一个测试使用的SDE函数
add_executable(${EXE_NAME} "src/examples/sde_black_scholes.cpp")
# 需要包含头文件路径
target_include_directories(${EXE_NAME}
	PUBLIC 
		${PROJECT_SOURCE_DIR}/src/models
		${PROJECT_SOURCE_DIR}/src
)
# 包含指定好位置的动态链接库
target_link_libraries(${EXE_NAME} ${SDE})
# 可执行文件目录必须直接存在.dll文件，否则将无法运行
file(COPY ${SDE} DESTINATION ${CMAKE_BINARY_DIR})
