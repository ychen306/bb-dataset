.PHONY: all clean

ifeq ($(NDEBUG), 1)
DEBUG_FLAG = -DNDEBUG=1
else
DEBUG_FLAG =
endif

CFLAGS = $(DEBUG_FLAG)
CC = /data/scratch/ychen306/gcc/gcc

all: test

test: test.o run_test.o rdpmc.o
	$(CC) -o $@ $^ -lrt

rdpmc.o: rdpmc.c

test.o: test.c

run_test.o: run_test.nasm bb.bin
	nasm -f elf64 -o $@ $< $(DEBUG_FLAG) -DREPS=$(REPS)

clean:
	rm -f run_test.o test.o rdpmc.o test
