OS := $(shell uname)
ifeq ($(OS),Darwin)
  CC = gcc-7
else
  CC = gcc
endif


CFLAGS = -c -g -std=c99 -Wall -O2

all: maitre
	./maitre

debug: maitre
	valgrind --leak-check=full --show-reachable=yes --track-fds=yes --track-origins=yes ./maitre

maitre: main.o operations.o socket.o simulation.o
	$(CC) -o maitre main.o operations.o socket.o simulation.o -lpthread

main.o: main.c
	$(CC) $(CFLAGS) main.c

operations.o: operations.c operations.h struct.h
	$(CC) $(CFLAGS) operations.c

socket.o: socket.c operations.o
	$(CC) $(CFLAGS) socket.c

simulation.o: simulation.c 
	$(CC) $(CFLAGS) simulation.c


clean:
	rm -f *.o
	rm -f *.gch
	rm -f main
