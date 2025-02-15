#plugin build file
cmake_minimum_required(VERSION 3.5.0)

#include common rules
include(../PluginRules.cmake)

#add sources, not including OpenEphysLib.cpp
add_sources(${PLUGIN_NAME}
	rhythm-api/rhd2000datablock.cpp
	rhythm-api/rhd2000evalboard.cpp
	rhythm-api/rhd2000registers.cpp
	UI/ChannelComponent.cpp
	UI/ChannelList.cpp
	UI/ChannelCanvas.cpp
	DeviceThread.cpp
	DeviceEditor.cpp
	AcqBoardOutput.cpp
	AcqBoardOutputEditor.cpp
	Headstage.cpp
	ImpedanceMeter.cpp
	)

if (MSVC)
	target_link_libraries(${PLUGIN_NAME} "${DLLDIR}/okFrontPanel.lib")
elseif(LINUX)
	target_link_libraries(${PLUGIN_NAME} "${DLLDIR}/libokFrontPanel.so")
elseif(APPLE)
	target_link_libraries(${PLUGIN_NAME} "${DLLDIR}/libokFrontPanel.dylib")
	set_source_files_properties(${DLLDIR}/libokFrontPanel.dylib PROPERTIES MACOSX_PACKAGE_LOCATION Frameworks)
	target_sources(${PLUGIN_NAME} PRIVATE ${DLLDIR}/libokFrontPanel.dylib)
endif()

#optional: create IDE groups
plugin_create_filters()
