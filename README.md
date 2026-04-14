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

When glicol-cli starts it prints every sample it loads together with its name, so you can check the full list in the console output.

## License

See [LICENSE](LICENSE).