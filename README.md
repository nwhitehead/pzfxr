
# PuzzleScript Sound Effectzor (PZFXR)

This is a command-line tool for converting [PuzzleScript](https://www.puzzlescript.net/)
sounds into WAV files. It aims to exactly match the random generation
used in PuzzleScript so the same seed will give identical patch parameters and
an identical final sound.


## Building

To build:
```bash
    mkdir build
    cd build
    cmake ..
    make
```

## Usage

```txt
PZSFXR : PuzzleScript Sound Effectzor

    -h, --help
        shows this help message
    -v, --verbose
        show verbose output
    -s, --seed
        set rng seed
    -o, --output
        write WAV output

EXAMPLE

    pzfxr --seed=27824302 --output=test.wav
```

## Credits

Written by Nathan Whitehead. Directly based on
the [PuzzleScript](https://www.puzzlescript.net/) code in
file `js/sfxr.js` by increpare. The PuzzleScript
sound generation functions are based on [BFXR](https://www.bfxr.net/)
by increpare, which is based on the original
[SFXR](http://www.drpetter.se/project_sfxr.html) by Thomas Petersson.
PZFXR uses [argagg](https://github.com/vietjtnguyen/argagg) by Viet The Nguyen
for command line parsing.
