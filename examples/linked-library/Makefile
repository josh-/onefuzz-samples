CC=clang
CFLAGS=-fsanitize=address,fuzzer -fPIC -O0 -ggdb3

.PHONY: all clean test

all: libbad1.so libbad2.so fuzz.exe

fuzz.exe: main.o libbad1.so libbad2.so
	$(CC) $(CFLAGS) -o $@ $< -lbad1 -lbad2 -L.

libbad1.so: bad1.o
	$(CC) -shared -o $@ $<
	
libbad2.so: bad2.o
	$(CC) -shared -o $@ $<
	
test: all
	LD_LIBRARY_PATH=. ./fuzz.exe

clean:
	rm -rf fuzz.exe *.o *.so crash-*
