# Hexdump crate

Crate to perform simple hexdump.

## Example

Create `main.rs` in `src`:

```rs
use std::fs::File;
use std::io::prelude::*;

use ::hexdump::hexdump;

fn main() -> std::io::Result<()> {
    let mut file = File::open("Cargo.toml")?;
    let mut contents = String::new();
    file.read_to_string(&mut contents)?;
    println!("Hexdump:\n{}", hexdump(contents, 8));
    Ok(())
}
```

```
Hexdump:
00000000|  5b 70 61 63  6b 61 67 65  |[package|
00000008|  5d 0a 6e 61  6d 65 20 3d  |].name =|
00000010|  20 22 68 65  78 64 75 6d  | "hexdum|
00000018|  70 22 0a 76  65 72 73 69  |p".versi|
00000020|  6f 6e 20 3d  20 22 30 2e  |on = "0.|
00000028|  31 2e 30 22  0a 65 64 69  |1.0".edi|
00000030|  74 69 6f 6e  20 3d 20 22  |tion = "|
00000038|  32 30 31 38  22 0a 0a 23  |2018"..#|
00000040|  20 53 65 65  20 6d 6f 72  | See mor|
00000048|  65 20 6b 65  79 73 20 61  |e keys a|
00000050|  6e 64 20 74  68 65 69 72  |nd their|
00000058|  20 64 65 66  69 6e 69 74  | definit|
00000060|  69 6f 6e 73  20 61 74 20  |ions at |
00000068|  68 74 74 70  73 3a 2f 2f  |https://|
00000070|  64 6f 63 2e  72 75 73 74  |doc.rust|
00000078|  2d 6c 61 6e  67 2e 6f 72  |-lang.or|
00000080|  67 2f 63 61  72 67 6f 2f  |g/cargo/|
00000088|  72 65 66 65  72 65 6e 63  |referenc|
00000090|  65 2f 6d 61  6e 69 66 65  |e/manife|
00000098|  73 74 2e 68  74 6d 6c 0a  |st.html.|
000000a0|  0a 5b 64 65  70 65 6e 64  |.[depend|
000000a8|  65 6e 63 69  65 73 5d 0a  |encies].|
```

Or using a wider version of 16 bytes per line:

```rs
use std::fs::File;
use std::io::prelude::*;

use ::hexdump::hexdump;

fn main() -> std::io::Result<()> {
    let mut file = File::open("Cargo.toml")?;
    let mut contents = String::new();
    file.read_to_string(&mut contents)?;
    println!("Hexdump:\n{}", hexdump(contents, 16));
    Ok(())
}
```

```
Hexdump:
00000000|  5b 70 61 63 6b 61 67 65  5d 0a 6e 61 6d 65 20 3d  |[package].name =|
00000010|  20 22 68 65 78 64 75 6d  70 22 0a 76 65 72 73 69  | "hexdump".versi|
00000020|  6f 6e 20 3d 20 22 30 2e  31 2e 30 22 0a 65 64 69  |on = "0.1.0".edi|
00000030|  74 69 6f 6e 20 3d 20 22  32 30 31 38 22 0a 0a 23  |tion = "2018"..#|
00000040|  20 53 65 65 20 6d 6f 72  65 20 6b 65 79 73 20 61  | See more keys a|
00000050|  6e 64 20 74 68 65 69 72  20 64 65 66 69 6e 69 74  |nd their definit|
00000060|  69 6f 6e 73 20 61 74 20  68 74 74 70 73 3a 2f 2f  |ions at https://|
00000070|  64 6f 63 2e 72 75 73 74  2d 6c 61 6e 67 2e 6f 72  |doc.rust-lang.or|
00000080|  67 2f 63 61 72 67 6f 2f  72 65 66 65 72 65 6e 63  |g/cargo/referenc|
00000090|  65 2f 6d 61 6e 69 66 65  73 74 2e 68 74 6d 6c 0a  |e/manifest.html.|
000000a0|  0a 5b 64 65 70 65 6e 64  65 6e 63 69 65 73 5d 0a  |.[dependencies].|
```

## Future improvements

Possible future improvements could include:

- Colorize output
- Add options to configure output (do not show offset, do not show ascii)
- Use of traits to support various input types. Currently supports `String` only