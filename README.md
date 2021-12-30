# XTEA

[![Build](https://github.com/runecore/xtea/workflows/build/badge.svg)](https://github.com/runecore/xtea)
[![API](https://docs.rs/extended-tea/badge.svg)](https://docs.rs/extended-tea)
[![Crate](https://img.shields.io/crates/v/extended-tea)](https://crates.io/crates/extended-tea)
[![dependency status](https://deps.rs/repo/github/runecore/xtea/status.svg)](https://deps.rs/repo/github/runecore/xtea)

This crate provides a Rusty implementation of the XTEA cipher, written in Rust.

This crate also provides convenience methods for ciphering and deciphering `u8` slices
and Read streams.

See [Wikipedia](https://en.wikipedia.org/wiki/XTEA) for more information on the XTEA cipher.

## Note

This crate should only be used if you're working on an existing application that uses XTEA.
If you're wanting to implement an encryption or a cipher system in your project DO NOT USE THIS.

## Installation

To use this crate, add the following to your `Cargo.toml`:

```toml
[dependencies]
extended-tea = "0.1.0"
```

## Example

```rust
use extended_tea::XTEA;
use byteorder::BE;

let input: Box<[u8]> = vec![10u8; 16].into_boxed_slice();

let xtea = XTEA::new([0x1380C5B5, 0x28037DF9, 0x26E314A2, 0xC57684E4]);

let encrypted = {
    let mut output = vec![0u8; input.len()].into_boxed_slice();
    xtea.encipher_u8slice::<BE>(&input, &mut output);
    output
};

let decrypted = {
    let mut output = vec![0u8; input.len()].into_boxed_slice();
    xtea.decipher_u8slice::<BE>(&encrypted, &mut output);
    output
};
assert_eq!(input, decrypted);
```
