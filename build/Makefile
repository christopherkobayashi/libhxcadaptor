#CC=i386-pc-linux-gcc
CC=gcc
AR=ar

UNAME := $(shell uname)

BASEDIR=../sources
INCLUDES = -I$(BASEDIR)/ -I ../../libhxcfe/sources -I ../../libusbhxcfe/sources

CFLAGS=-O3 $(INCLUDES)
LDFLAGS= -g -shared -lc -lm  -ldl
EXEC=libhxcadaptor.a

# For shared libraries:
# EXEC=libhxcadaptor.so
# CFLAGS += -fPIC (in per-platform overrides)

ifeq ($(UNAME), Linux)
CFLAGS += -fPIC
endif

ifeq ($(UNAME), Darwin)
CFLAGS += -arch i386 -mmacosx-version-min=10.5
LDFLAGS += -arch i386 -mmacosx-version-min=10.5
endif

all: $(EXEC)

libhxcadaptor.a: libhxcadaptor.o fs.o
	$(AR) r $@    $^
	mkdir -p ../../build
	cp $@ ../../build/

libhxcadaptor.o: $(BASEDIR)/libhxcadaptor.c
	$(CC) -o $@ -c $< $(CFLAGS)

fs.o: $(BASEDIR)/fs.c
	$(CC) -o $@ -c $< $(CFLAGS)

clean:
	rm -rf *.o

mrproper: clean
	rm -rf $(EXEC)

.PHONY: clean mrproper
