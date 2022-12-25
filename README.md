# VE.Direct library for Rust

[![crates.io badge][crate_badge]][crate]
[![docs.rs badge][docs_badge]][docs]

Library to parse the Victron Energy "VE.Direct" protocol and map the data to useful structs with clear units.

Can be used in conjuction with the `serial` library to pull battery status information from devices like the BMV 700, or solar charging data from the Victron's various MPPT solar charge controllers.

[crate_badge]: https://img.shields.io/crates/v/vedirect
[crate]: https://crates.io/crates/vedirect
[docs]: https://docs.rs/vedirect/
[docs_badge]: https://docs.rs/vedirect/badge.svg

## Details

Developed using a VE.Direct to USB interface cable. Based of the `VE.Direct-Protocol-3.32.pdf`.

The following Device Status Messages are implemented to spec:

* MPPT

Currently only implements the "Text-mode" (read only) interface,

> The VE.Direct interface includes two modes: Text-mode and the HEX-mode. The purpose of the Text-mode is to make retrieving information extremely simple. The product will periodically transmit all run-time fields. The HEX-mode allows not only to read data but also write data, for example, change settings.

**Note** If you are manually reading data off the Serial Port, as the given example demonstrates, data is written in 1 second intervals. If you read the buffer quicker or slower than this, you will either get incomplete or multiple sets of data.

## Testing

The project has tests which can be run by usual `cargo test`

Additionally, there is a basic fuzzing setup for the parser which can be run easily using [`cargo-afl`](https://crates.io/crates/afl) - see `fuzz-target/run-fuzzer.sh`

## Status

Functional and reasonably well tested. Main limitation is that not all devices are handled, only the BMV battery monitor and solar charge controllers
