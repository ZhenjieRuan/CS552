CC = gcc
CFLAGS = -m32 -fno-builtin -fno-stack-protector -fno-strict-aliasing -fno-delete-null-pointer-checks -nostdinc -I. -g -Wall -std=c99
CPPFLAGS = -Wa,--32 -MMD
OBJS = boot.o fifos.o print.o interrupt.o
PROGS = fifos-1
MNT_POINT=/mnt/

all: $(PROGS)

fifos-1: $(OBJS)
	$(LD) -m elf_i386 -T fifos.ld -o $@ $^

boot.o: boot.S
	$(CC) $(CFLAGS) -c boot.S

fifos.o: fifos.c
	$(CC) $(CFLAGS) -c fifos.c

print.o: print.c
	$(CC) $(CFLAGS) -c print.c

interrupt.o: interrupt.c
	$(CC) $(CFLAGS) -c interrupt.c

clean:
	rm fifos-1 boot.o fifos.o print.o interrupt.o

test:
	qemu-system-i386 -kernel fifos-1 -m 256

