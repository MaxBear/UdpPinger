CPPFLAGS=-std=c++14 
THRIFT_GEN+= -Igen-cpp
CPP=g++
LDFLAGS=-g $(THRIFT_GEN)
LDLIBS=-lfolly -lgflags -lpthread -lthrift -ldouble-conversion -lglog -ldl -liberty -levent
THRIFT=thrift

all: uping

uping: UdpPinger Pinger_types.o Pinger_constants.o
	$(CPP) $(LDFLAGS) $(CPPFLAGS) Pinger_constants.o Pinger_types.o UdpPinger.o Main.cpp -o uping $(LDLIBS)

UdpPinger: gen-cpp
	$(CPP) $(LDFLAGS) $(CPPFLAGS) -c  UdpPinger.cpp

gen-cpp:
	$(THRIFT) -r --gen cpp Pinger.thrift

Pinger_types.o: gen-cpp
	$(CPP) $(LDFLAGS) $(CPPFLAGS) -c gen-cpp/Pinger_types.cpp

Pinger_constants.o: gen-cpp
	$(CPP) $(LDFLAGS) $(CPPFLAGS) -c gen-cpp/Pinger_constants.cpp

clean:
	rm -f *.o uping
	rm -rf ./gen-cpp
