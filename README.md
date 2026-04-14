# glicol_demo

A demo project for [Glicol](https://glicol.org) live coding using [glicol-cli](https://github.com/glicol/glicol-cli).

## Prerequisites

- [Rust / Cargo](https://doc.rust-lang.org/cargo/getting-started/installation.html)

## Installation

### 1. Clone the repository (with samples)

This repo includes the [Dirt-Samples](https://github.com/tidalcycles/Dirt-Samples) as a git submodule in the `samples/` directory. Clone with `--recurse-submodules` to fetch them automatically:

```sh
git clone --recurse-submodules https://github.com/<your-user>/glicol_demo.git
cd glicol_demo
```

If you already cloned without `--recurse-submodules`, initialise the submodule manually:

```sh
git submodule update --init
```

### 2. Install glicol-cli

```sh
cargo install --git https://github.com/glicol/glicol-cli.git
```

## Running the demo

Point `glicol-cli` at the bundled samples and start playing `test.glicol`:

```sh
export GLICOL_CLI_SAMPLES_PATH=./samples
glicol-cli test.glicol
```

Edit `test.glicol` in your favourite editor and changes are picked up in real-time.

## Sample naming

`glicol-cli` builds sample names from the Dirt-Samples directory structure using the pattern `\{folder}{filestem}`. For example:

| File on disk               | Sample name in Glicol |
|----------------------------|-----------------------|
| `samples/bd/BT0A0D0.wav`  | `\bdBT0A0D0`         |
| `samples/cp/HANDCLP0.wav` | `\cpHANDCLP0`        |
| `samples/hh27/hh27closedhh.wav` | `\hh27000_hh27closedhh` |
| `samples/sid/000_bas2.wav` | `\sid000_bas2`       |

**Note:** `glicol-cli` only loads files with lowercase extensions (`.wav`, `.mp3`, `.ogg`). Some Dirt-Samples directories (e.g. `808/`, `808bd/`) use uppercase `.WAV` and are therefore skipped. The demo uses samples from directories that have lowercase extensions.

## Finding and using samples

### Listing all available samples

When `glicol-cli` starts it prints every sample it loads. Run in headless mode and filter for the list:

```sh
GLICOL_CLI_SAMPLES_PATH=./samples glicol-cli -H test.glicol 2>&1 | grep "Adding sample"
```

This prints one line per sample, e.g. `Adding sample: \bdBT0A0D0`.

### Browsing by category

The `samples/` directory is organised into folders by instrument or sound type. Some useful ones:

| Folder      | Contents                 |
|-------------|--------------------------|
| `bd/`       | Bass drums / kicks       |
| `sd/`       | Snare drums              |
| `cp/`       | Claps                    |
| `hh/`       | Hi-hats                  |
| `hh27/`     | Hi-hats (alt set)        |
| `sid/`      | SID chip sounds          |
| `cb/`       | Cowbells                 |
| `cr/`       | Crashes                  |
| `tabla/`    | Tabla percussion         |
| `realclaps/`| Real clap recordings     |
| `bass/`     | Bass hits                |
| `stab/`     | Stab synths              |
| `pluck/`    | Plucked strings          |
| `jazz/`     | Jazz kit                 |

To see all available folders:

```sh
ls samples/
```

To see the files (and therefore the available sample names) inside a folder:

```sh
ls samples/bd/
```

Each file becomes a sample named `\{folder}{filestem}`, so `samples/bd/BT0A0D0.wav` is used in Glicol code as `sp \bdBT0A0D0`.

### Searching for a specific sound

Use `grep` to search the loaded sample list for keywords:

```sh
GLICOL_CLI_SAMPLES_PATH=./samples glicol-cli -H test.glicol 2>&1 \
  | grep "Adding sample" | grep -i kick
```

### Using a sample in your code

Once you know the sample name, use `sp` (sample playback) in your `.glicol` file:

```
~kick: speed 4.0 >> seq 60 >> sp \bdBT0A0D0
~hat: speed 8.0 >> seq 60 >> sp \hh27000_hh27closedhh >> mul 0.5
~clap: seq 0 _60 0 _60 >> sp \cpHANDCLP0 >> mul 0.7

out: mix ~kick ~hat ~clap >> plate 0.1
```

The `seq` node triggers the sample (`60` = play, `0` = silence, `_` = rest). Use `speed` to control the step rate and `mul` to adjust volume.

## License

See [LICENSE](LICENSE).