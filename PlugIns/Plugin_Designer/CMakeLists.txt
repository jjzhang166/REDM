#-------------------------------------------------------
# Copyright (c) DuiMagic
# All rights reserved.
# History:
# 		<Author>	<Time>		<Version>	  <Des>
#      guoyou		2016-11-13	1.0		
#-------------------------------------------------------
PROJECT(Plugin_Designer)

# �ļ����飨���ˣ���ͬʱ������뵽ADD_LIBRARY�в�����ʾ
FILE(GLOB ROOT_HEADER 							inc/*.h)
FILE(GLOB ROOT_SOURCE 							src/*.cpp;src/*.c)

SOURCE_GROUP("inc" 								FILES 	${ROOT_HEADER})
SOURCE_GROUP("src"								FILES 	${ROOT_SOURCE})

 # ����Ԥ����ͷ
use_precompiled_header(Plugin_Designer
   "${CMAKE_CURRENT_SOURCE_DIR}/inc/Plugin_DesignerAfx.h"
   "${CMAKE_CURRENT_SOURCE_DIR}/src/Plugin_DesignerAfx.cpp"
  )
  
# ����ͷ�ļ�����·��
INCLUDE_DIRECTORIES(${CMAKE_CURRENT_SOURCE_DIR}/inc;)

# ����DmMain��ͷ�ļ�
INCLUDE_DIRECTORIES(${DM_SOURCE_DIR}/DmMain/inc
					${DM_SOURCE_DIR}/DmMain/inc/Common;
					${DM_SOURCE_DIR}/DmMain/inc/Common/Template;
					${DM_SOURCE_DIR}/DmMain/inc/Core;
					${DM_SOURCE_DIR}/DmMain/inc/Core/Msg;
					${DM_SOURCE_DIR}/DmMain/inc/Core/Dui;
					${DM_SOURCE_DIR}/DmMain/inc/Core/Event;
					${DM_SOURCE_DIR}/DmMain/inc/IDmMain;
					${DM_SOURCE_DIR}/DmMain/inc/Modules;
					${DM_SOURCE_DIR}/DmMain/inc/Widgets;)
					
# ����Plugin_Designer��ͷ�ļ�
INCLUDE_DIRECTORIES(${DM_SOURCE_DIR}/PlugIns/Plugin_Designer/inc)

# �������
add_definitions(-DUNICODE -D_UNICODE)  # unicode�汾
set(CMAKE_DEBUG_POSTFIX "_d")		   # Debug�������ļ����Ӻ�׺,��exe��Ч.

# �������·����Plugins/��֧��
set(LIBRARY_OUTPUT_PATH  ${DM_BINARY_DIR}/bin/plugins)

ADD_LIBRARY(Plugin_Designer SHARED 
			${ROOT_HEADER};
			${ROOT_SOURCE};
			)

# �������·����Plugins/��֧��
set_target_properties(Plugin_Designer PROPERTIES ARCHIVE_OUTPUT_DIRECTORY_DEBUG ${DM_BINARY_DIR}/bin/plugins)
set_target_properties(Plugin_Designer PROPERTIES RUNTIME_OUTPUT_DIRECTORY_DEBUG ${DM_BINARY_DIR}/bin/plugins)
set_target_properties(Plugin_Designer PROPERTIES ARCHIVE_OUTPUT_DIRECTORY_RELEASE ${DM_BINARY_DIR}/bin/plugins)
set_target_properties(Plugin_Designer PROPERTIES RUNTIME_OUTPUT_DIRECTORY_RELEASE ${DM_BINARY_DIR}/bin/plugins)
set_target_properties(Plugin_Designer PROPERTIES ARCHIVE_OUTPUT_DIRECTORY_MINSIZEREL  ${DM_BINARY_DIR}/bin/plugins)
set_target_properties(Plugin_Designer PROPERTIES RUNTIME_OUTPUT_DIRECTORY_MINSIZEREL  ${DM_BINARY_DIR}/bin/plugins)
set_target_properties(Plugin_Designer PROPERTIES ARCHIVE_OUTPUT_DIRECTORY_RELWITHDEBINFO  ${DM_BINARY_DIR}/bin/plugins)
set_target_properties(Plugin_Designer PROPERTIES RUNTIME_OUTPUT_DIRECTORY_RELWITHDEBINFO  ${DM_BINARY_DIR}/bin/plugins)
#set_target_properties(Plugin_Designer PROPERTIES LINKER_LANGUAGE CXX)#���CMake can not determine linker language for target

# ������Ŀ������
add_dependencies(Plugin_Designer  DmMain)

SET_TARGET_PROPERTIES(Plugin_Designer PROPERTIES FOLDER PlugIns)