# vim: ts=4:sw=4:expandtab
CMAKE_MINIMUM_REQUIRED(VERSION 3.18...3.23)

PROJECT(libgambatte
	LANGUAGES C CXX)
ADD_LIBRARY(${PROJECT_NAME}
	src/bitmap_font.cpp
	src/cpu.cpp
	src/gambatte.cpp
	src/initstate.cpp
	src/interrupter.cpp
	src/interruptrequester.cpp
	src/loadres.cpp
	src/memory.cpp
	src/sound.cpp
	src/state_osd_elements.cpp
	src/statesaver.cpp
	src/tima.cpp
	src/video.cpp
	src/mem/cartridge.cpp
	src/mem/memptrs.cpp
	src/mem/pakinfo.cpp
	src/mem/rtc.cpp
	src/sound/channel1.cpp
	src/sound/channel2.cpp
	src/sound/channel3.cpp
	src/sound/channel4.cpp
	src/sound/duty_unit.cpp
	src/sound/envelope_unit.cpp
	src/sound/length_counter.cpp
	src/video/ly_counter.cpp
	src/video/lyc_irq.cpp
	src/video/next_m0_time.cpp
	src/video/ppu.cpp
	src/video/sprite_mapper.cpp)
TARGET_INCLUDE_DIRECTORIES(${PROJECT_NAME} PRIVATE ./src ./include ../common)
ADD_COMPILE_DEFINITIONS(HAVE_STDINT_H)

FIND_PACKAGE(ZLIB)

IF(ZLIB_FOUND)
	TARGET_SOURCES(${PROJECT_NAME} src/file/unzip/unzip.c
		src/file/unzip/ioapi.c
		src/file/file_zip.cpp)
	TARGET_INCLUDE_DIRECTORIES(${PROJECT_NAME} ZLIB_INCLUDE_DIRS)
	TARGET_LINK_LIBRARIES(${PROJECT_NAME} ZLIB_LIBRARIES)
ELSE()
	TARGET_SOURCES(${PROJECT_NAME} PRIVATE src/file/file.cpp)
ENDIF()
