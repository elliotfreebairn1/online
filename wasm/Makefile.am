
noinst_LIBRARIES = libonline.a

libonline_a_SOURCES = \
	../common/Authorization.cpp \
	../common/ConfigUtil.cpp \
	../common/FileUtil.cpp \
	../common/CommandControl.cpp \
	../common/Log.cpp \
	../common/MessageQueue.cpp \
	../common/TraceEvent.cpp \
	../common/Protocol.cpp \
	../common/StringVector.cpp \
	../common/Session.cpp \
	../common/SigUtil.cpp \
	../common/SpookyV2.cpp \
	../common/Unit.cpp \
	../common/Util.cpp \
	../common/CommandControl.cpp \
	../kit/ChildSession.cpp \
	../kit/Kit.cpp \
	../net/FakeSocket.cpp \
	../net/Socket.cpp \
	../wsd/ClientSession.cpp \
	../wsd/DocumentBroker.cpp \
	../wsd/COOLWSD.cpp \
	../wsd/RequestDetails.cpp \
	../wsd/Storage.cpp \
	../wsd/TileCache.cpp

AM_CXXFLAGS = \
	-pthread -s USE_PTHREADS=1 \
	-s DISABLE_EXCEPTION_CATCHING=0

AM_CPPFLAGS = \
	-I$(top_srcdir) \
	-I$(top_srcdir)/common \
	-I$(top_srcdir)/kit \
	-I$(top_srcdir)/net \
	-I$(top_srcdir)/wsd \
	-I@LOBUILDDIR@/workdir/UnpackedTarball/libpng \
	-I@LOBUILDDIR@/workdir/UnpackedTarball/zlib \
	-DCOOLWSD_CONFIGDIR='"@COOLWSD_CONFIGDIR@"' \
	-DMOBILEAPP=1

bin_PROGRAMS = online

online_SOURCES = wasmapp.cpp

online_DEPENDENCIES = \
	libonline.a

# note cannot add .linkdeps to DEPENDENCIES because it contains -lFoo
online_LDADD = \
	libonline.a \
	${POCOLIB}/libPocoEncodings@POCODEBUG@.a \
	${POCOLIB}/libPocoNet@POCODEBUG@.a \
	${POCOLIB}/libPocoUtil@POCODEBUG@.a \
	${POCOLIB}/libPocoXML@POCODEBUG@.a \
	${POCOLIB}/libPocoJSON@POCODEBUG@.a \
	${POCOLIB}/libPocoFoundation@POCODEBUG@.a \
	${ZSTDLIB}/libzstd.a \
	-L@LOBUILDDIR@/instdir/program \
	$(shell cat @LOBUILDDIR@/instdir/program/soffice.html.linkdeps)

# TODO these are just copypasta from core
# TODO still missing --pre-js flags, which are needed?
online_LDFLAGS = \
	-pthread -s USE_PTHREADS=1 -s TOTAL_MEMORY=1GB -s PTHREAD_POOL_SIZE=4 --bind -s FORCE_FILESYSTEM=1 -s WASM_BIGINT=1 -s ERROR_ON_UNDEFINED_SYMBOLS=1 -s FETCH=1 -s ASSERTIONS=1 -s EXIT_RUNTIME=0 -s EXPORTED_RUNTIME_METHODS=["UTF16ToString","stringToUTF16","UTF8ToString","allocateUTF8","printErr","ccall","cwrap","FS"] -pthread -s USE_PTHREADS=1 -s DISABLE_EXCEPTION_CATCHING=0 -s EXPORTED_FUNCTIONS=["_main","_libreofficekit_hook","_libreofficekit_hook_2","_lok_preinit","_lok_preinit_2","_doc_postUnoCommand"]