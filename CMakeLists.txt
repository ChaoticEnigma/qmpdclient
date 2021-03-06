cmake_minimum_required(VERSION 3.15)

project(QMPDClient C CXX)

find_package(Qt5 REQUIRED COMPONENTS Core Widgets Network Xml XmlPatterns DBus X11Extras LinguistTools)

if(APPLE)
	# ??
elseif(UNIX)
	find_package(X11 REQUIRED)
endif()

set(CMAKE_INCLUDE_CURRENT_DIR TRUE)
set(CMAKE_AUTOMOC TRUE)

if(WIN32)
	set(QT_USE_QTMAIN TRUE)
endif()

if(NOT DEFINED VERSION)
	find_program(GIT_CMD git)
	execute_process(COMMAND "${GIT_CMD}" describe
		OUTPUT_VARIABLE VERSION
		OUTPUT_STRIP_TRAILING_WHITESPACE
		)
	if(NOT VERSION)
		set(VERSION 1.2.2)
	endif()
	message(STATUS "Current version: ${VERSION}")
endif()

set(NAMEVER "QMPDClient ${VERSION}")

set(QMPDClient_srcs
	src/aafilter.cpp
	src/aboutdialog.cpp
	src/abstractmodel.cpp
	src/abstractview.cpp
	src/albumview.cpp
	src/artistview.cpp
	src/clickablelabel.cpp
	src/config.cpp
	src/controlpanel.cpp
	src/coverartdialog.cpp
	src/directorymodel.cpp
	src/directorypanel.cpp
	src/directoryview.cpp
	src/dynamicplaylist.cpp
	src/fileview.cpp
	src/headerview.cpp
	src/idealbar.cpp
	src/idealsplitter.cpp
	src/lastfmsubmitter.cpp
	src/libmpdclient.c
	src/librarypanel.cpp
	src/lineedit.cpp
	src/lyricsdialog.cpp
	src/mainwindow.cpp
	src/metainfodialog.cpp
	src/mpdcache.cpp
	src/mpdconnection.cpp
	src/mpd.cpp
	src/mpddirectory.cpp
	src/mpdentities.cpp
	src/mpdoutput.cpp
	src/mpdsong.cpp
	src/mpdsonglist.cpp
	src/mpdsongmodel.cpp
	src/mpdsongview.cpp
	src/mpdstats.cpp
	src/mpdstatus.cpp
	src/notifications.cpp
	src/passivepopup.cpp
	src/pausabletimer.cpp
	src/playlistitemdelegate.cpp
	src/playlistmodel.cpp
	src/playlistpanel.cpp
	src/playlistspanel.cpp
	src/playlistsview.cpp
	src/playlistview.cpp
	src/plconview.cpp
	src/plsfile.cpp
	src/preferencesdialog.cpp
	src/qmpdclient.cpp
	src/radiopanel.cpp
	src/radioview.cpp
	src/reconnect.cpp
	src/serverinfo.cpp
	src/servermodel.cpp
	src/shortcutmodel.cpp
	src/shortcuts.cpp
	src/shoutcastmodel.cpp
	src/shoutcastpanel.cpp
	src/shoutcastview.cpp
	src/shoutcastfetcher.cpp
	src/shoutcaststation.cpp
	src/songview.cpp
	src/stringlistmodel.cpp
	src/stringlistview.cpp
	src/tagguesser.cpp
	src/tagmodel.cpp
	src/timelabel.cpp
	src/timeslider.cpp
	src/trayicon.cpp
	src/traysonginfo.cpp
	src/verticalbutton.cpp

	#    src/qmpdclient_mac.cpp
	#    src/qmpdclient_win.cpp
	#    src/qmpdclient_x11.cpp
	#    src/notifications_dbus.cpp
	#    src/notifications_nodbus.cpp

	src/aafilter.h
	src/aboutdialog.h
	src/abstractmodel.h
	src/abstractview_defn.h
	src/abstractview.h
	src/abstractview_impl.h
	src/albumview.h
	src/artistview.h
	src/clickablelabel.h
	src/config.h
	src/controlpanel.h
	src/coverartdialog.h
	src/debug.h
	src/directorymodel.h
	src/directorypanel.h
	src/directoryview.h
	src/dynamicplaylist.h
	src/fileview.h
	src/headerview.h
	src/idealbar.h
	src/idealsplitter.h
	src/lastfmsubmitter.h
	src/libmpdclient.h
	src/librarypanel.h
	src/lineedit.h
	src/lyricsdialog.h
	src/macroexpander.h
	src/mainwindow.h
	src/metainfodialog.h
	src/mpdcache.h
	src/mpdcache_p.h
	src/mpdconnection.h
	src/mpddirectory.h
	src/mpdentities.h
	src/mpd.h
	src/mpdoutput.h
	src/mpd_p.h
	src/mpdsong.h
	src/mpdsonglist.h
	src/mpdsongmodel.h
	src/mpdsongview.h
	src/mpdstats.h
	src/mpdstatus.h
	src/notifications.h
	src/passivepopup.h
	src/pausabletimer.h
	src/playlistitemdelegate.h
	src/playlistmodel.h
	src/playlistpanel.h
	src/playlistspanel.h
	src/playlistsview.h
	src/playlistview.h
	src/plconview.h
	src/plsfile.h
	src/preferencesdialog.h
	src/qmpdclient.h
	src/radiopanel.h
	src/radioview.h
	src/reconnect.h
	src/richtext.h
	src/serverinfo.h
	src/servermodel.h
	src/shortcutmodel.h
	src/shortcuts.h
	src/shoutcastpanel.h
	src/shoutcastview.h
	src/shoutcastmodel.h
	src/shoutcastfetcher.h
	src/shoutcaststation.h
	src/songview.h
	src/stringlistmodel.h
	src/stringlistview.h
	src/tagguesser.h
	src/tagmodel.h
	src/timelabel.h
	src/timeslider.h
	src/trayicon.h
	src/traysonginfo.h
	src/verticalbutton.h
	)

qt5_wrap_ui(QMPDClient_ui_srcs
	ui/aboutdialog.ui
	ui/addradiodialog.ui
	ui/controlpanel.ui
	ui/coverartdialog.ui
	ui/directorypanel.ui
	ui/librarypanel.ui
	ui/lyricsdialog.ui
	ui/mainwindow.ui
	ui/metainfodialog.ui
	ui/playlistpanel.ui
	ui/playlistspanel.ui
	ui/preferencesdialog.ui
	ui/radiopanel.ui
	ui/shoutcastpanel.ui
	)

set(TS_FILES
	lang/cs_CZ.ts
	lang/de_DE.ts
	lang/es_ES.ts
	lang/fr_FR.ts
	lang/it_IT.ts
	lang/nl_NL.ts
	lang/nn_NO.ts
	lang/no_NO.ts
	lang/pt_BR.ts
	lang/ru_RU.ts
	lang/sv_SE.ts
	lang/tr_TR.ts
	lang/uk_UA.ts
	lang/zh_CN.ts
	lang/zh_TW.ts
	)

set_source_files_properties(${TS_FILES} PROPERTIES OUTPUT_LOCATION "${CMAKE_CURRENT_BINARY_DIR}/l10n")
qt5_add_translation(COMPILED_TRANSLATIONS ${TS_FILES})

add_executable(qmpdclient
	${QMPDClient_srcs}
	${QMPDClient_ui_srcs}
	qmpdclient.qrc
	${COMPILED_TRANSLATIONS}
	)

set_target_properties(qmpdclient PROPERTIES AUTORCC ON)

target_link_libraries(qmpdclient Qt5::Widgets Qt5::Network Qt5::Xml Qt5::XmlPatterns Qt5::DBus Qt5::X11Extras)

if(WIN32)
	target_link_libraries(qmpdclient ws2_32)
	set_target_properties(qmpdclient PROPERTIES WIN32_EXECUTABLE TRUE)
elseif(APPLE)
	# ??
else()
	target_link_libraries(qmpdclient ${X11_LIBRARIES})
endif()

target_include_directories(qmpdclient PRIVATE
	${CMAKE_CURRENT_BINARY_DIR}
	src
	)

target_compile_definitions(qmpdclient PRIVATE
	NAMEVER="${NAMEVER}"
	PREFIX="${CMAKE_INSTALL_PREFIX}"
	VERSION="${VERSION}"
	)

if(WIN32)
	target_sources(qmpdclient PRIVATE
		src/notifications_nodbus.cpp
		src/qmpdclient_win.cpp icons/resource.rc
		)
elseif(APPLE)
	target_sources(qmpdclient PRIVATE
		src/notifications_nodbus.cpp
		src/qmpdclient_mac.cpp
		)
else()
	if(Qt5DBus_FOUND)
		message(STATUS "QtDBus found")
		#        set(QT_USE_QTDBUS TRUE)
		target_sources(qmpdclient PRIVATE
			src/notifications_dbus.cpp
			src/qdbus_adaptor.cpp
			src/qdbus_adaptor.h
			)
		target_compile_definitions(qmpdclient PRIVATE
			WITH_DBUS
			)
	else()
		message(STATUS "QtDBus not found")
		target_sources(qmpdclient PRIVATE
			src/notifications_nodbus.cpp
			)
	endif()

	target_sources(qmpdclient PRIVATE
		src/qmpdclient_x11.cpp
		)
endif()


if(WIN32)
	install(TARGETS qmpdclient DESTINATION .)
	install(FILES ${COMPILED_TRANSLATIONS} DESTINATION translations)
else()
	install(TARGETS qmpdclient DESTINATION bin)
	install(FILES qmpdclient.desktop DESTINATION share/applications)
	install(FILES icons/64x64/qmpdclient.png DESTINATION share/icons/hicolor/64x64/apps/)
	install(FILES icons/48x48/qmpdclient.png DESTINATION share/icons/hicolor/48x48/apps/)
	install(FILES icons/22x22/qmpdclient.png DESTINATION share/icons/hicolor/22x22/apps/)
	install(FILES icons/16x16/qmpdclient.png DESTINATION share/icons/hicolor/16x16/apps/)
	install(FILES icons/svg/qmpdclient.svg DESTINATION share/icons/hicolor/scalable/apps/)
	install(FILES ${COMPILED_TRANSLATIONS} DESTINATION share/QMPDClient/translations)
endif()
