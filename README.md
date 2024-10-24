# `reorient-circular-seq`

`reorient-circular-seq` is a tool designed to reorient circular DNA sequences to prevent the truncation of genes that span the sequence's endpoints. Here's a concise overview of its process:

1. **Gene prediction**: [`pyrodigal-gv`](https://github.com/althonos/pyrodigal-gv) is used to predict genes within the circular DNA sequence.
2. **Assessment of truncated genes**: The tool checks if the first and/or last predicted genes are split by the current linear breakpoint.
3. **Shift breakpoint**: Rotates the sequence to move the breakpoint to the center of the longest intergenic (between two CDSs) region.
4. **Iterate if necessary**: The gene prediction is run again on the reoriented sequence. If truncated genes are still exist, the breakpoint is shifted to the next longest intergenic region. This process repeats until a configuration with no truncated genes is found or all intergenic regions have been tried.

By systematically adjusting the breakpoint to optimal intergenic areas, `reorient-circular-seq` tries to increase the amount of genes are fully intact in the linear representation.

## Installation

```sh
$ git clone https://github.com/apcamargo/reorient-circular-seq.git
$ cd reorient-circular-seq
$ pixi run reorient-circular-seq -h
```

## Usage

```sh
$ reorient-circular-seq [OPTIONS] [INPUT] [OUTPUT]
```

### Positional arguments

| Argument | Description                                |
| :------- | :----------------------------------------- |
| `input`  | Input FASTA file (default: stdin)          |
| `output` | Output FASTA file (default: stdout)        |

### Options

| Option            | Short | Value type            | Description                                                                                             | Default          |
|:------------------|:------|:----------------------|:--------------------------------------------------------------------------------------------------------|------------------|
| `--remove-tr`     |       |                       | Trim terminal repeats from the ends of the sequences.                                                   |                  |
| `--min-tr-length` |       | Integer (≥1)          | Minimum length of the terminal repeat to be removed. Only used if `--remove-tr` is set.                 | `21`             |
| `--threads`       | `-t`  | Integer (1–16)        | Number of threads to use.                                                                               | `4`              |
| `--verbose`       | `-v`  | Integer (0–2)         | Verbosity level.                                                                                        | `0`              |
| `--help`          | `-h`  |                       | Show this message and exit.                                                                             |                  |
