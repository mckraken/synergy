# synergy -- mouse and keyboard sharing utility
# Copyright (C) 2012-2016 Symless Ltd.
# Copyright (C) 2009 Nick Bolton
#
# This package is free software; you can redistribute it and/or
# modify it under the terms of the GNU General Public License
# found in the file LICENSE that should have accompanied this file.
#
# This package is distributed in the hope that it will be useful,
# but WITHOUT ANY WARRANTY; without even the implied warranty of
# MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the
# GNU General Public License for more details.
#
# You should have received a copy of the GNU General Public License
# along with this program.  If not, see <http://www.gnu.org/licenses/>.

set(sources
	synergyc.cpp
)

if (WIN32)
	file(GLOB arch_headers "MSWindows*.h")
	file(GLOB arch_sources "MSWindows*.cpp")
	list(APPEND sources
		resource.h
		synergyc.ico
		synergyc.rc
		tb_error.ico
		tb_idle.ico
		tb_run.ico
		tb_wait.ico
	)
elseif (APPLE)
	file(GLOB arch_headers "OSX*.h")
	file(GLOB arch_sources "OSX*.cpp")
elseif (UNIX)
	file(GLOB arch_headers "XWindows*.h")
	file(GLOB arch_sources "XWindows*.cpp")
endif()

if (SYNERGY_ADD_HEADERS)
	list(APPEND sources ${headers})
	list(APPEND sources ${arch_headers})
endif()

include_directories(
	../
	../../lib/
)

add_executable(synergyc ${sources} ${arch_sources})
target_link_libraries(synergyc
	arch base client io mt net ipc platform server synlib ${libs} ${OPENSSL_BOTH_LIBS})
