README
Overview
This script processes FASTQ files by demultiplexing them into sample-specific FASTQ files based on nucleotide patterns and rules defined in a CSV file. The script extracts a region of each read depending on a specified start pattern, an optional contain pattern, and an optional insert length.

Requirements
Python 3

Biopython (for handling FASTQ file parsing and sequence manipulation)

Standard Python libraries: csv, re, and glob

Input Files
Demultiplex.csv

This CSV file should contain a header and the following columns for each sample:

sample_name: Identifier for the sample.

start_pattern: The starting nucleotide pattern to search for in each read.

contain_pattern (optional): A pattern that must be present after the start pattern. Uses 'N' as a wildcard matching any nucleotide.

insert_length (optional): Number of bases to extract after the start pattern. If set to 0 or left blank, the behavior varies:

If a contain pattern is provided, the script extracts the sequence between the start pattern and the contain pattern.

If no contain pattern is provided and insert length is 0, the script extracts all sequence from the end of the start pattern to the end of the read.

If insert length is greater than 0 without a contain pattern, exactly that number of bases is extracted.

FASTQ Files

Place all FASTQ files you wish to process in the same directory as the script.

Note: The script excludes FASTQ files that are generated as output (i.e., files named <sample_name>.fastq).

Output Files
Sample FASTQ Files:
For each sample specified in the CSV file, a separate FASTQ file (named <sample_name>.fastq) is created containing the trimmed reads assigned to that sample.

read_assignment_counts.txt:
This file contains a summary of the read assignments. It includes counts of reads assigned for each input FASTQ file and a total count per sample.

Unique Sequences Files:
For each sample, a text file named <sample_name>_unique_sequences.txt is created. This file lists unique deplexed sequences along with their counts.

How to Use
Prepare the Input Files:

Edit the Demultiplex.csv file to include the appropriate pattern rules for your samples.

Place all input FASTQ files (excluding output files) in the working directory.

Run the Script:
Execute the script using Python:

bash
Copy
python your_script_name.py
Replace your_script_name.py with the actual name of the script file.

Review the Outputs:

Check the sample-specific FASTQ files for correctly trimmed reads.

Open read_assignment_counts.txt to verify the assignment counts per file and overall.

Review each <sample_name>_unique_sequences.txt file for a breakdown of unique sequences.

Additional Notes
The script automatically adjusts quality scores (if available) when trimming reads.

If no contain pattern is provided, different extraction rules apply based on the provided insert length.

Ensure that the output FASTQ filenames do not conflict with the names of the input FASTQ files.

For any modifications or troubleshooting, review the inline code logic relating to how patterns are converted into regex objects.
