server:
	@cargo build --release
	@rust-objcopy --strip-all target/riscv64gc-unknown-none-elf/release/myos -O binary target/riscv64gc-unknown-none-elf/release/myos.bin
	@qemu-system-riscv64 \
    -machine virt \
    -nographic \
    -bios ../bootloader/rustsbi-qemu.bin \
    -device loader,file=target/riscv64gc-unknown-none-elf/release/myos.bin,addr=0x80200000 \
    -s -S

client:
	@riscv64-unknown-elf-gdb \
    -ex 'file target/riscv64gc-unknown-none-elf/release/myos' \
    -ex 'set arch riscv:rv64' \
    -ex 'target remote localhost:1234'

clean:
	@cargo clean
