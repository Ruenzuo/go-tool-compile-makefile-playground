LINK_TARGET := main

LLVM_POSTFIX := -5.0
LLVM_CONFIG := llvm-config$(LLVM_POSTFIX)
LLVM_BINDIR := $(shell $(LLVM_CONFIG) --bindir)
ifeq ($(LLVM_BINDIR),)
  $(error llvm-config needs to be installed)
endif

ifeq ($(strip $(LIBTRANSISTOR_HOME)),)
$(error "Please set LIBTRANSISTOR_HOME in your environment. export LIBTRANSISTOR_HOME=<path to libtransistor>")
endif

include $(LIBTRANSISTOR_HOME)/libtransistor.mk

# CC := $(LLVM_BINDIR)/clang
CTC := go tool compile

OBJ := main.o

all: $(LINK_TARGET).nro.so

%.o: %.cpp
	$(CXX) $(CXX_FLAGS) -Wno-pointer-arith -c -o $@ $<

# %.o: %.go
# 	$(CTC) $<

$(LINK_TARGET).nro.so: ${OBJ} $(LIBTRANSITOR_NRO_LIB) $(LIBTRANSISTOR_COMMON_LIBS)
	$(LD) $(LD_FLAGS) -lSDL2 -o $@ ${OBJ} $(LIBTRANSISTOR_NRO_LDFLAGS)

