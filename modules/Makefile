# https://www.studentrobotics.org/trac/wiki/Beagleboard_DSP/Building

LLVM_CONFIGURE_FLAGS ?= --target tic64x --program-prefix tic64x- --prefix $(PREFIX)
BINUTILS_CONFIGURE_FLAGS ?= --prefix $(PREFIX)

NEWLIB_CONFIGURE_FLAGS ?= --host=tic64x --with-newlib \
	CC="clang -ccc-host-triple tms320c64x-unknown-unknown" \
	CC_FOR_TARGET="clang -ccc-host-triple tms320c64x-unknown-unknown" \
	CC_FOR_BUILD="clang -ccc-host-triple tms320c64x-unknown-unknown" \
	AR=tic64x-ar \
	AS=tic64x-as \
	PONIES=true

tic6x-binutils-build: tic6x-binutils
	@mkdir -p binutils-build && cd binutils-build && \
	../$</configure $(BINUTILS_CONFIGURE_FLAGS) && \
					$(MAKE) && $(MAKE) install

llvm-tic6x-build: llvm-tic6x
	@cd $</tools && ln -s ../../clang-tic6x clang && \
	cd - && mkdir llvm-build && cd llvm-build && \
	../$</configure $(LLVM_CONFIGURE_FLAGS) && \
					$(MAKE) && $(MAKE) install

newlib-tic6x-build: newlib-tic6x
	@mkdir -p newlib-build && cd newlib-build && \
	../$</configure $(NEWLIB_CONFIGURE_FLAGS) && \
					$(MAKE) &&
	tic64x-ranlib tic64x/newlib/libc/libc.a
	${info If this has failed, use prebuilt binary in dsp-examples!}

