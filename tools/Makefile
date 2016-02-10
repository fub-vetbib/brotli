#brotli/tools

include ../shared.mk

BROTLI = ..
ENCOBJ = $(BROTLI)/enc/*.o
DECOBJ = $(BROTLI)/dec/*.o

EXECUTABLES=bro brzip

EXE_OBJS=$(patsubst %, %.o, $(EXECUTABLES))

all : $(EXECUTABLES) links

tests: links brzip
	./brot-test.sh

# Create hard-links for brot (similar to bzcat bunbzip2)
links: brzip
	ln -f brzip brcat
	ln -f brzip brunzip

$(EXECUTABLES) : $(EXE_OBJS) deps
	$(CXX) $(LDFLAGS) $(ENCOBJ) $(DECOBJ) $@.o -o $@

deps :
	$(MAKE) -C $(BROTLI)/dec
	$(MAKE) -C $(BROTLI)/enc nodict

clean :
	rm -f $(OBJS) $(EXE_OBJS) $(EXECUTABLES)
	$(MAKE) -C $(BROTLI)/dec clean
	$(MAKE) -C $(BROTLI)/enc clean
