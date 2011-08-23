# https://www.studentrobotics.org/trac/wiki/Beagleboard_DSP/Building

TARGET_ARCH = tic6x

LLVM_CONFIGURE_FLAGS ?= --target $(TARGET_ARCH) --program-prefix $(TARGET_ARCH)- --prefix $(PREFIX)
BINUTILS_CONFIGURE_FLAGS ?= --program-prefix $(TARGET_ARCH)- --prefix $(PREFIX)

NEWLIB_CONFIGURE_FLAGS ?= --host=$(TARGET_ARCH) --with-newlib \
	CC="clang -ccc-host-triple tms320c64x-unknown-unknown" \
	CC_FOR_TARGET="clang -ccc-host-triple tms320c64x-unknown-unknown" \
	CC_FOR_BUILD="clang -ccc-host-triple tms320c64x-unknown-unknown" \
	AR=$(TARGET_ARCH)-ar \
	AS=$(TARGET_ARCH)-as \
	PONIES=true

$(TARGET_ARCH)-binutils-build: $(TARGET_ARCH)-binutils
	@mkdir -p binutils-build && cd binutils-build && \
	../$</configure $(BINUTILS_CONFIGURE_FLAGS) && \
					$(MAKE) && $(MAKE) install

llvm-$(TARGET_ARCH)-build: llvm-$(TARGET_ARCH)
	@cd $</tools && ln -s ../../clang-$(TARGET_ARCH) clang && \
	cd - && mkdir llvm-build && cd llvm-build && \
	../$</configure $(LLVM_CONFIGURE_FLAGS) && \
					$(MAKE) && $(MAKE) install

newlib-$(TARGET_ARCH)-build: newlib-$(TARGET_ARCH)
	@mkdir -p newlib-build && cd newlib-build && \
	../$</configure $(NEWLIB_CONFIGURE_FLAGS) && \
					$(MAKE) &&
	$(TARGET_ARCH)-ranlib $(TARGET_ARCH)/newlib/libc/libc.a
	${info If this has failed, use prebuilt binary in dsp-examples!}

