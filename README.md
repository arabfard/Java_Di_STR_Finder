# STRsMiner - Repetitive Sequence Detection Tool

**STRsMiner** is a Java-based tool designed for detecting short tandem repeats (STRs) in genomic DNA sequences. The algorithm supports two detection modes: overlapping and non-overlapping. This tool can be used to identify repetitive sequences with customizable repeat core lengths and repeat counts.

---

## 🔍 Algorithm Description

### ✅ Overlapping Mode (`true`)
In this mode, after reading the input genome file, the algorithm processes the sequence nucleotide by nucleotide. From each position:

1. It checks for the **longest repetitive sequence** starting with a **single-nucleotide core**.
2. If a repeat is found, it is recorded.
3. The algorithm then checks for longer cores (e.g., dinucleotides, trinucleotides, etc.) starting from the same nucleotide.
4. This continues until no more valid repeats can be found from that position.
5. The process then advances by one nucleotide and repeats until the end of the genome sequence is reached.

This mode **allows overlapping** between detected repeat regions.

### 🚫 Non-Overlapping Mode (`false`)
In this mode, the process is similar to the overlapping mode, but with a key difference:

- As soon as a valid repeat is found from a position, the algorithm **skips forward** by the length of the detected repeat and starts checking from the new position.
- This ensures that overlapping repeat regions are ignored, which may increase speed and avoid redundancy.

---

## ⚙️ How to Run the Program

### ✅ Prerequisites
Ensure that **Java Runtime Environment (JRE)** is installed on your machine.

### ▶️ Execution Command

```bash
java -jar STRsMiner-Module.jar <input file> <min core length> <max core length> <min repeat of core> <max repeat of core> <with overlap or not>
```

### Example:
```bash
java -jar STRsMiner-Module.jar chr.txt 1 6 3 20 true
```

---

## 🔡 Command Line Arguments

| Argument               | Description                                                                 |
|------------------------|-----------------------------------------------------------------------------|
| `<input file>`         | Path to the input genome sequence file                                      |
| `<min core length>`    | Minimum length of the repeat core unit (e.g., 1 for mononucleotide)          |
| `<max core length>`    | Maximum length of the repeat core unit (e.g., 6 for hexanucleotide)          |
| `<min repeat of core>` | Minimum number of times the core must repeat                                |
| `<max repeat of core>` | Maximum number of times the core is allowed to repeat                       |
| `<with overlap or not>`| Whether to allow overlapping in repeat detection (`true` or `false`)        |

---

## 📂 Sample Input

The input file should be a plain text file in FASTA format. For example:

**File: `chr.txt`**
```
>chr1
NNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNN
NNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNN
aaaaaaaaaaAAAAAAAAAAtatatatatatatatatatcatcatcatca
gctggcagctagggacattgcagggtcctcttgctcaaggtgtagtggca
gcacgcccacctgctggcagctggggacactgccgggccctcttgctCCA
ACAGTACTGGCGGATTATAGGGAAACACCCGGAGCATATGCTGTTTGGTC
TCAGtagactcctaaatatgggattcctgggtttaaaagtaaaaaataaa
```

---

## 📤 Sample Output

The program generates an output file with the same name as the input file but with a `.out` extension (e.g., `chr.out`). Each line in the output represents a detected repeat with the following columns:

```
<core>  <repeat_count>  <formatted_repeat>  <start_position>  <end_position>
```

Example output:

**File: `chr.out`**
```
a       10      (a)10      100     109
A       10      (A)10      110     119
ta      9       (ta)9      120     137
tca     4       (tca)4     138     149
a       6       (a)6       340     345
a       13      (a)13      347     359
```
