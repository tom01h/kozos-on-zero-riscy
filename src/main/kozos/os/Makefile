PREFIX  = $(HOMEPATH)/bin/riscv64-unknown-elf-gcc-20171231-x86_64-w64-mingw32
ARCH    = riscv64-unknown-elf
BINDIR  = $(PREFIX)/bin
ADDNAME = $(ARCH)-

AR      = $(BINDIR)/$(ADDNAME)ar.exe
AS      = $(BINDIR)/$(ADDNAME)as.exe
CC      = $(BINDIR)/$(ADDNAME)gcc.exe
LD      = $(BINDIR)/$(ADDNAME)ld.exe
NM      = $(BINDIR)/$(ADDNAME)nm.exe
OBJCOPY = $(BINDIR)/$(ADDNAME)objcopy.exe
OBJDUMP = $(BINDIR)/$(ADDNAME)objdump.exe
RANLIB  = $(BINDIR)/$(ADDNAME)ranlib.exe
STRIP   = $(BINDIR)/$(ADDNAME)strip.exe

OBJS  = startup.o main.o
OBJS += lib.o serial.o

TARGET = kozos

CFLAGS = -Wall -nostdinc -nostdlib -fno-builtin -march=rv32im -mabi=ilp32
CFLAGS += -I.
#CFLAGS += -g
CFLAGS += -O
CFLAGS += -DKOZOS

LFLAGS = -static -n -T ld.scr -L.

.SUFFIXES: .c .o
.SUFFIXES: .s .o

all :		$(TARGET)

$(TARGET) :	$(OBJS)
		$(CC) $(OBJS) -o $(TARGET) $(CFLAGS) $(LFLAGS)
		copy $(TARGET) $(TARGET).elf
		$(STRIP) $(TARGET)

.c.o :		$<
		$(CC) -c $(CFLAGS) $<

.s.o :		$<
		$(CC) -c $(CFLAGS) $<

clean :
		del $(OBJS) $(TARGET) $(TARGET).elf
