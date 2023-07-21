# Getting Started

!!! warning

    Documentation is still a work-in-progress!

RustSmith at it's core is simply an executable that will run and generate programs based on command-line arguments passed in. Follow the steps below to start the generation of programs!

## Getting the executable

### Recommended Method

To download and install RustSmith, the recommended method is to simply download the "RustSmith
Executable" from the latest release from the "Releases" panel on the right.

RustSmith can then be invoked as below:

```shell
./rustsmith --help
```

### Docker

Docker can also be used in the following way using the latest docker image:

```shell
docker run --rm ghcr.io/rustsmith/rustsmith --help
```

### Running RustSmith using the JAR File

Alternatively, the JAR file in the releases can be downloaded and used instead. RustSmith would then
be invoked as:

```shell
java -jar RustSmith-1.0-SNAPSHOT-all.jar
```

### Building from Source

To build RustSmith from source, an installation of Java 15 is required. More information for
installing OpenJDK 15 can be found on the [OpenJDK Website](https://openjdk.java.net).

Building and executing RustSmith can then be done as follows:

```shell
git clone git@github.com:rustsmith/rustsmith.git
cd rustsmith
./gradlew build
```

This will create both the standalone executable under `./run/rustsmith` and the packaged JAR file
under `./build/libs/RustSmith-1.0-SNAPSHOT-all.jar` which can then be executed as described above.

## Basic Usage of Rustsmith

### Run command

RustSmith is just a command line tool that can generate you valid Rust programs randomly.

The most basic usage of rustsmith would be the following command:

```shell
./rustsmith -n 1
```

### Folder structure of output

Which, when ran, should set up a folder structure wherever you ran the program in the following way:

```shell
./outRust
|-- file0
|   |-- file0.rs
|   |-- file0.txt
```

Depending on the number of files you want to generate (specified by the `-n` flag) the number of programs will increase.

Within each folder there are 2 main files: `fileX.rs` and `fileX.txt`.

 - **`file0.rs`** is the valid and automatically generated rust file!
 - **`file0.txt`** is the list of _command line arguments_ that should be passed into the executable

### Example file output

`file0.rs` will look something like the following:
 
??? note "Generated Rust Program snippet"

    ```rust
    #![allow(warnings, unused, unconditional_panic)]
    use std::env;
    use std::collections::hash_map::DefaultHasher;
    use std::hash::{Hash, Hasher};
    const CONST1: f32 = 0.2419321f32;
    const CONST2: i128 = 131415789711622847644195956159839136052i128;
    const CONST3: u8 = 173u8;
    const CONST4: f32 = 0.32691818f32;
    const CONST5: bool = false;
    const CONST6: u32 = 2727919348u32;
    const CONST7: u32 = 1813123347u32;
    const CONST8: i128 = 53614034395947885105180317431878184857i128;
    const CONST9: f32 = 0.41204387f32;
    const CONST10: u16 = 887u16;
    macro_rules! reconditioned_mod{
        ($a:expr,$b:expr, $zero: expr) => {
            {
                let denominator = $b;
                if (denominator != $zero) {($a % denominator)} else {$zero}
            }
        }
    }
    macro_rules! reconditioned_div{
        ($a:expr,$b:expr, $zero: expr) => {
            {
                let denominator = $b;
                if (denominator != $zero) {($a / denominator)} else {$zero}
            }
        }
    }
    macro_rules! reconditioned_access{
        ($a:expr,$b:expr) => {{
            let arrLength = $a.len();
            let index = $b;
            $a[if (index < arrLength) { index } else { 0 }]
        }};
    }
    #[derive(Debug)]
    struct Struct2 {
    var6: Option<u32>,
    var7: f32,
    var8: i32,
    var9: u8,
    }

    impl Struct2 {
    #[inline(never)]
    fn fun7(&self, var41: f64, var42: Option<u16>, var43: i128, var44: Option<Struct2>, hasher: &mut DefaultHasher) -> Struct3 {
    44i8;
    ();
    138654581908947122899287364284989451186i128;
    let var45: u16 = 34348u16;
    Struct2 {var6: None::<u32>, var7: 0.7830445f32, var8: 899283879i32, var9: 227u8,};
    let mut var46: i128 = 74743375548520924870409283084422405671i128;
    var46 = 28713462321172602643073431590454312989i128;
    1517252645i32;
    735464689u32;
    0.7460238032098697f64;
    format!("{:?}", var41).hash(hasher);
    format!("{:?}", var44).hash(hasher);
    vec![0.8649663464953213f64,0.05053026936017313f64,0.8529252322989213f64,0.0075586315580329355f64];
    ();
    ........
    ```

This is your first randomly generated, valid, Rust program!

### Testing the generated rust file

This can then be compiled against rustc and run with the command line arguments:

```shell
> rustc file0.rs

> ./file0.rs 0.78968924 159490765721744842190015396263998969651 104585524602189803966499020697899014819 RRDoKHc 4442417947899502423 8901 true -1624219412 89 0.16808917087337594 -4799608715056474785 # input from 1.txt

Program Seed: 8760012246522298462
7619823349681210740
```

The output produces the following 2 lines of output always:

 - **Program Seed**: this is a seed used throughout the generation process for all random selections taken in the program. The idea is you can reproduce the same program through rustsmith by using the seed printed here (through the `-s <SEED>` option!)
 - **Hashed output**: this number is the **hash** of all variables in scope by the end of the program _along with_ any other variables that were randomly chosen in the generation of the program to be added to the hasher. This is the main number to compare when running _differential testing_ across different optimization levels and compilers.

## Usage options in RustSmith

```shell
Usage: rustsmith [OPTIONS]

Options:
  -n, -count INT    No. of files to generate
  -p, -print        Print out program only
  -f, -fail-fast    Use fail fast approach
  -s, -seed INT     Optional Seed
  --directory TEXT  Directory to save files
  -h, --help        Show this message and exit
```
