# Makefile for building the tock kernel for the HiFive1 platform

TARGET=riscv32imac-unknown-none-elf
PLATFORM=hifive1

include ../Makefile.common

flash: $(TOCK_ROOT_DIRECTORY)target/$(TARGET)/release/$(PLATFORM).elf
	openocd \
		-c "source [find board/sifive-hifive1.cfg]; flash protect 0 64 last off; program $<; resume 0x20400000; exit"

qemu: $(TOCK_ROOT_DIRECTORY)target/$(TARGET)/release/$(PLATFORM).elf
	qemu-system-riscv32 -M sifive_e -kernel $^  -nographic

qemu-app: $(TOCK_ROOT_DIRECTORY)target/$(TARGET)/release/$(PLATFORM).elf
	qemu-system-riscv32 -M sifive_e -kernel $^ -device loader,file=$(APP),addr=0x20430000 -nographic
