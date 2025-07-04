bionic = $(top_srcdir)/common/q/bionic
bionic_libc = $(bionic)/libc

modlibexecdir = $(libdir)/libhybris/linker
modlibexec_LTLIBRARIES = q.la

ARCH_FLAGS =

AM_CFLAGS = \
	-std=gnu99

AM_CPPFLAGS = \
	-fno-stack-protector \
	-Wstrict-overflow=5

AM_CXXFLAGS = \
	-std=gnu++11 \
	-Wold-style-cast

q_la_SOURCES = \
	hybris_compat.cpp \
	bionic/libc/bionic/bionic_call_ifunc_resolver.cpp \
	dlfcn.cpp \
	linker_allocator.cpp \
	linker_block_allocator.cpp \
	linker.cpp \
	linker_cfi.cpp \
	linker_config.cpp \
	linker_dlwarning.cpp \
	linker_gdb_support.cpp \
	linker_globals.cpp \
	linker_logger.cpp \
	linker_main.cpp \
	linker_mapped_file_fragment.cpp \
	linker_memory.cpp \
	linker_namespaces.cpp \
	linker_phdr.cpp \
	linker_sdk_versions.cpp \
	linker_soinfo.cpp \
	linker_tls.cpp \
	linker_utils.cpp \
	rt.cpp \
	../strlcpy.c \
	../strlcat.c \
	bionic/libc/bionic/bionic_elf_tls.cpp \
	bionic/libc/bionic/bionic_allocator.cpp

if WANT_ARCH_ARM64
q_la_SOURCES += \
	tlsdesc_resolver.S
endif

q_la_CPPFLAGS = \
	$(AM_CPPFLAGS) \
	-I$(top_srcdir)/include \
	-I$(top_srcdir)/common \
	-I$(bionic_libc)/ \
	-I$(bionic_libc)/include \
	-DDEFAULT_HYBRIS_LD_LIBRARY_PATH="\"@DEFAULT_HYBRIS_LD_LIBRARY_PATH@\"" \
	-D_USING_LIBCXX \
	$(ARCH_FLAGS) \
	$(ANDROID_HEADERS_CFLAGS)

if HAS_ANDROID_11_0_0
q_la_CPPFLAGS += -DHAS_ANDROID_11_0_0
endif

q_la_LDFLAGS = \
	-lpthread \
	-lsupc++ \
	-module \
	-avoid-version

if WANT_DEBUG
q_la_CPPFLAGS += \
	-DTRACE_DEBUG=1
else
q_la_CPPFLAGS += \
	-DTRACE_DEBUG=1
endif

if WANT_ARM_TRACING
q_la_CPPFLAGS += \
	-DWANT_ARM_TRACING
endif
