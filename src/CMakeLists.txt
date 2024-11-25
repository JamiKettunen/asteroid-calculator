if(NOT WITH_MAPPLAUNCHERD)
qt_add_executable(asteroid-calculator)
endif()

qt_add_qml_module(asteroid-calculator
	URI asteroidapp
	QML_FILES
		Display.qml
		CalcButton.qml
		calculator.js
		main.qml
	SOURCES
		main.cpp
	NO_PLUGIN
	#ENABLE_TYPE_COMPILER
)

if(WITH_MAPPLAUNCHERD)
set_target_properties(asteroid-calculator PROPERTIES PREFIX "")
endif()

target_link_libraries(asteroid-calculator PUBLIC
	AsteroidApp)

# TODO: drop debug once AOT produces less warnings etc
set_target_properties(asteroid-calculator PROPERTIES QT_QMLCACHEGEN_ARGUMENTS "--verbose")

install(TARGETS asteroid-calculator
	DESTINATION $<IF:$<BOOL:${WITH_MAPPLAUNCHERD}>,${CMAKE_INSTALL_LIBDIR},${CMAKE_INSTALL_BINDIR}>)
