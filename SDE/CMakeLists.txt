cmake_minimum_required (VERSION 3.8)

project (getSDELibs)
# ����.exe���ļ���
set(EXE_NAME "testSDE01")
# # ����.dll������λ�ã�Ĭ���Ǻ�bin��ͬ
# set(LIBRARY_OUTPUT_PATH ${PROJECT_SOURCE_DIR}/lib)

# ����src�������ļ������.cpp�ļ�
file(GLOB LIB_SRC
	"src/*.cpp"
	"src/models/*.cpp"
)

# ����һ����̬���ӿ�
add_library(SDE SHARED ${LIB_SRC})
# ��Ҫ����ͷ�ļ�·��
target_include_directories(SDE
	PUBLIC 
		${PROJECT_SOURCE_DIR}/src/models
		${PROJECT_SOURCE_DIR}/src
)

# # add_subdirectory(src)
# # find_library(SDE "libSDE.dll" PATHS "${PROJECT_SOURCE_DIR}/lib")

# # ����ʵ�ڲ��Ҳ���libSDE.dll����˲���ֱ���趨�ļ�λ�õķ���
# set(SDE "${PROJECT_SOURCE_DIR}/lib/libSDE.dll")

# ����һ������ʹ�õ�SDE����
add_executable(${EXE_NAME} "src/examples/simple_sde.cpp")
# ��Ҫ����ͷ�ļ�·��
target_include_directories(${EXE_NAME}
	PUBLIC 
		${PROJECT_SOURCE_DIR}/src/models
		${PROJECT_SOURCE_DIR}/src
)
# �����Ѿ�����õĶ�̬���ӿ�
target_link_libraries(${EXE_NAME} SDE)
# # ��ִ���ļ�Ŀ¼����ֱ�Ӵ���.dll�ļ��������޷�����
# file(COPY ${SDE} DESTINATION ${CMAKE_BINARY_DIR})