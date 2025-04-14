# FASTQ Demultiplexing Script

## 🧬 Overview
This script processes FASTQ files by demultiplexing them into sample-specific FASTQ files based on nucleotide patterns and rules defined in a CSV file. It extracts regions of each read depending on a specified start pattern, an optional contain pattern, and an optional insert length.

---

## 📦 Requirements
- Python 3
- [Biopython](https://biopython.org/) (for handling FASTQ parsing and sequence manipulation)
- Standard Python libraries: `csv`, `re`, and `glob`

---

## 📂 Input Files

### `Demultiplex.csv`
This CSV file should include a header row and the following columns for each sample:

- `sample_name`: Identifier for the sample.
- `start_pattern`: Nucleotide pattern to match at the start of a read.
- `contain_pattern` *(optional)*: A sequence that must appear after the start pattern. 'N' is treated as a wildcard.
- `insert_length` *(optional)*: Number of bases to extract after the start pattern.

**Extraction behavior based on insert length and contain pattern:**
- If `contain_pattern` is provided: extracts sequence between `start_pattern` and `contain_pattern`.
- If `insert_length = 0` or blank and no `contain_pattern`: extracts from the end of `start_pattern` to the end of the read.
- If `insert_length > 0` and no `contain_pattern`: extracts that number of bases from the end of the start pattern.

### FASTQ Files
Place all input FASTQ files to be processed in the same directory as the script.

> ⚠️ Output FASTQ files (named `<sample_name>.fastq`) will be skipped if present in the directory.

---

## 📤 Output Files

- **Sample FASTQ Files**:  
  Each sample in the CSV gets a file named `<sample_name>.fastq` with the demultiplexed and trimmed reads.

- **`read_assignment_counts.txt`**:  
  Summarizes how many reads from each input FASTQ file were assigned to each sample.

- **Unique Sequences Files**:  
  For each sample, a file named `<sample_name>_unique_sequences.txt` lists all unique sequences and their counts.

---

## ▶️ How to Use

1. **Prepare Input Files**
   - Edit `Demultiplex.csv` with pattern rules for each sample.
   - Place all input FASTQ files in the same directory as the script.

2. **Run the Script**

   ```bash
   python your_script_name.py
