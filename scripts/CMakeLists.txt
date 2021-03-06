#
# Copyright (C) 2016-2018 Draios Inc dba Sysdig.
#
# This file is part of falco .
#
# Licensed under the Apache License, Version 2.0 (the "License");
# you may not use this file except in compliance with the License.
# You may obtain a copy of the License at
#
#     http://www.apache.org/licenses/LICENSE-2.0
#
# Unless required by applicable law or agreed to in writing, software
# distributed under the License is distributed on an "AS IS" BASIS,
# WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
# See the License for the specific language governing permissions and
# limitations under the License.
#
configure_file(debian/postinst.in debian/postinst)
configure_file(debian/prerm.in debian/prerm)

if(NOT SYSDIG_DIR)
	set(SYSDIG_DIR "${PROJECT_SOURCE_DIR}/../sysdig")
endif()

file(COPY "${PROJECT_SOURCE_DIR}/scripts/debian/falco"
	DESTINATION "${PROJECT_BINARY_DIR}/scripts/debian")

file(COPY "${PROJECT_SOURCE_DIR}/scripts/rpm/falco"
	DESTINATION "${PROJECT_BINARY_DIR}/scripts/rpm")

if(CMAKE_SYSTEM_NAME MATCHES "Linux")
	install(PROGRAMS ${SYSDIG_DIR}/scripts/sysdig-probe-loader
		DESTINATION ${FALCO_BIN_DIR}
		RENAME falco-probe-loader)
endif()
