cmake_minimum_required (VERSION 3.8)

project (getSDELibs)
# ����.exe���ļ���
set(EXE_NAME "testSDE02")
# ����.dll������λ�ã�Ĭ���Ǻ�bin��ͬ
 set(LIBRARY_OUTPUT_PATH ${PROJECT_SOURCE_DIR}/lib)

# ����src�������ļ������.cpp�ļ�
file(GLOB LIB_SRC
	"src/*.cpp"
	"src/models/*.cpp"
)

# # add_subdirectory(src)
# # find_library(SDE "libSDE.dll" PATHS "${PROJECT_SOURCE_DIR}/lib")

# ����ʵ�ڲ��Ҳ���libSDE.dll����˲���ֱ���趨�ļ�λ�õķ���
set(SDE "${PROJECT_SOURCE_DIR}/lib/libSDE.dll")

# ����һ������ʹ�õ�SDE����
add_executable(${EXE_NAME} "src/examples/sde_black_scholes.cpp")
# ��Ҫ����ͷ�ļ�·��
target_include_directories(${EXE_NAME}
	PUBLIC 
		${PROJECT_SOURCE_DIR}/src/models
		${PROJECT_SOURCE_DIR}/src
)
# ����ָ����λ�õĶ�̬���ӿ�
target_link_libraries(${EXE_NAME} ${SDE})
# ��ִ���ļ�Ŀ¼����ֱ�Ӵ���.dll�ļ��������޷�����
file(COPY ${SDE} DESTINATION ${CMAKE_BINARY_DIR})