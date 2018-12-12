CPPFLAGS=-std=c++14 
THRIFT_GEN+= -Igen-cpp
CPP=g++
LDFLAGS=-g $(THRIFT_GEN)
LDLIBS=-lfolly -lgflags -lpthread -lthrift -ldouble-conversion -lglog -ldl -liberty -levent
THRIFT=/usr/local/bin/thrift

prefix=/usr/local

all: uping

uping: UdpPinger Pinger_types.o Pinger_constants.o
	$(CPP) $(LDFLAGS) $(CPPFLAGS) src/Pinger_constants.o src/Pinger_types.o src/UdpPinger.o src/Main.cpp -o src/uping $(LDLIBS)

UdpPinger: gen-cpp
	$(CPP) $(LDFLAGS) $(CPPFLAGS) -c src/UdpPinger.cpp -o src/UdpPinger.o

gen-cpp:
	$(THRIFT) -r -o src --gen cpp src/Pinger.thrift

Pinger_types.o: gen-cpp
	$(CPP) $(LDFLAGS) $(CPPFLAGS) -c src/gen-cpp/Pinger_types.cpp -o src/Pinger_types.o

Pinger_constants.o: gen-cpp
	$(CPP) $(LDFLAGS) $(CPPFLAGS) -c src/gen-cpp/Pinger_constants.cpp -o src/Pinger_constants.o

install: src/uping
	install -D src/uping \
		$(DESTDIR)$(prefix)/bin/uping

clean:
	rm -f src/*.o src/uping
	rm -rf src/gen-cpp

distclean: clean

uninstall:
	-rm -f $(DESTDIR)$(prefix)/bin/uping
