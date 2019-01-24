cmake_minimum_required (VERSION 3.12)
project (ircd)

set (CMAKE_BUILD_TYPE Debug)

set (ircd_AVBANLEN 40)
set (ircd_BUFFERPOOL 27000000)
set (ircd_CONNECTFREQUENCY 600)
set (ircd_CONNECTTIMEOUT 90)
set (ircd_CPATH "ircd.conf")
set (ircd_DOMAINNAME "myircd")
set (ircd_DPATH ".")
set (ircd_DBPATH "database")
set (ircd_DEFAULTMAXSENDQLENGTH 40000)
set (ircd_HANGONGOODLINK 300)
set (ircd_HANGONRETRYDELAY 10)
set (ircd_LOGPATH "/dev/null")
set (ircd_MAXCHANNELSPERUSER 5)
set (ircd_MPATH "ircd.motd")
set (ircd_KILLCHASETIMELIMIT 30)
set (ircd_MAXCONNECTIONS 2048)
set (ircd_MAXIMUM_LINKS 1)
set (ircd_MAXWATCH 96)
set (ircd_NICKNAMEHISTORYLENGTH MAXCONNECTIONS/25)
set (ircd_PINGFREQUENCY 120)
set (ircd_PORTNUM 6667)
set (ircd_RPATH "remote.motd")
set (ircd_MAXSILES 15)
set (ircd_MAXSILELENGTH MAXSILES*AVBANLEN)
set (ircd_SPATH "ircd")

IF(CMAKE_BUILD_TYPE MATCHES Debug)
    set (ircd_DEBUGMODE 1)
    set (ircd_LPATH "/tmp/ircd.log")
    set (ircd_LOGPATH LPATH)
ENDIF()

configure_file (
  "config/config.h.in"
  "include/config.h"
)

# This builds version.c
execute_process(COMMAND /bin/sh version.c.SH WORKING_DIRECTORY "src/ircd")

include_directories("include")

file(GLOB ircd_sources src/ircd/*)
list(FILTER ircd_sources EXCLUDE REGEX "chkconf.c")

set(EXECUTABLE_OUTPUT_PATH "build")
add_executable(ircd ${ircd_sources})
target_link_libraries(ircd event json-c resolv z)
