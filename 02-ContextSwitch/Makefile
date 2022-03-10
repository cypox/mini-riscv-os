# from: https://github.com/riscv-collab/riscv-gnu-toolchain/releases/download/2022.03.09/riscv64-elf-ubuntu-20.04-nightly-2022.03.09-nightly.tar.gz
RISCVPATH=../../gnu-toolchain/riscv64-elf/bin/
CC = $(RISCVPATH)riscv64-unknown-elf-gcc
CFLAGS = -nostdlib -fno-builtin -mcmodel=medany -march=rv32ima -mabi=ilp32
#CFLAGS = -nostdlib -fno-builtin -mcmodel=medany -march=rv64id -mabi=lp64d

QEMU = qemu-system-riscv32
QFLAGS = -nographic -smp 4 -machine virt -bios none

OBJDUMP = riscv64-unknown-elf-objdump

all: os.elf

os.elf: start.s sys.s lib.c os.c
	$(CC) $(CFLAGS) -T os.ld -o os.elf $^

qemu: $(TARGET)
	@qemu-system-riscv32 -M ? | grep virt >/dev/null || exit
	@echo "Press Ctrl-A and then X to exit QEMU"
	$(QEMU) $(QFLAGS) -kernel os.elf

clean:
	rm -f *.elf
