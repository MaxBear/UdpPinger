CPPFLAGS=-std=c++14
THRIFT_GEN+= -Igen-cpp
CPP=g++
LDFLAGS=-g $(THRIFT_GEN)
LDLIBS=-lfolly -lgflags -lpthread -lglog -ldouble-conversion -liberty
THRIFT=/usr/local/bin/thrift

prefix=/usr/local

all: upong

upong: NoradTargetThread.o
	$(CPP) $(LDFLAGS) $(CPPFLAGS) src/NoradTargetThread.o src/Main.cpp -o src/upong $(LDLIBS)

NoradTargetThread.o:
	$(CPP) $(LDFLAGS) $(CPPFLAGS) -c  src/NoradTargetThread.cpp -o src/NoradTargetThread.o

install: src/upong
	install -D src/upong \
		$(DESTDIR)$(prefix)/bin/upong

clean:
	rm -f src/*.o src/upong

distclean: clean

uninstall:
	-rm -f $(DESTDIR)$(prefix)/bin/upong
