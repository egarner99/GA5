## Trial #1: 

**AI Tool** - GitHub Copilot

**Question #1:** Write a simple script to run files through trimgalore.

**Code Provided:**

**Results #1:**
















## Trial #5: 

**AI Tool** - GitHub Copilot

**Question 1:** How do I write a script to download and rename files from the SRA Explorer at the same time?

**Code Provided:** 

It created a script called download_sra.sh: 
```bash
#!/bin/bash

# Check if the input file exists
if [ $# -ne 1 ]; then
    echo "Usage: ./download_sra.sh input_file.txt"
    echo "The input file should contain lines in the format: URL,new_filename"
    exit 1
fi

input_file=$1

# Check if the input file exists
if [ ! -f "$input_file" ]; then
    echo "Error: Input file $input_file not found!"
    exit 1
fi

# Create a downloads directory if it doesn't exist
mkdir -p downloads

# Read the input file line by line
while IFS=',' read -r url new_name || [ -n "$url" ]; do
    # Skip empty lines
    if [ -z "$url" ]; then
        continue
    fi
    
    echo "Downloading $new_name from $url"
    wget -q --show-progress "$url" -O "downloads/$new_name"
    
    if [ $? -eq 0 ]; then
        echo "Successfully downloaded and renamed to $new_name"
    else
        echo "Error downloading $url"
    fi
done < "$input_file"

echo "All downloads completed!"
```


It also gave me a code to make the script executable: `chmod +x download_sra.sh`, to change the permissions as it was originally `-rw-rw---`.

Additionally, it said to make a text file `sra_downloads.txt` with the desired URLs and filenames, which just had the two urls: `ftp://ftp.sra.ebi.ac.uk/vol1/fastq/SRR247/027/SRR24727827/SRR24727827_1.fastq.gz ftp://ftp.sra.ebi.ac.uk/vol1/fastq/SRR247/027/SRR24727827/SRR24727827_2.fastq.gz`

It then said to run the script using `./download_sra.sh sra_downloads.txt`

**Result #1:**

The code didn't seem to really work, unless I missed a step. All it did was create the downloads dir. It looks like a missed a step, so I allowed it to create an example input file based on its suggestion.

**Prompt #2:** Yes, create an example input file with the urls ftp://ftp.sra.ebi.ac.uk/vol1/fastq/SRR247/027/SRR24727827/SRR24727827_1.fastq.gz
ftp://ftp.sra.ebi.ac.uk/vol1/fastq/SRR247/027/SRR24727827/SRR24727827_2.fastq.gz

**Code Provided:**
It changed my sra_downloads.txt file: 
```bash
ftp://ftp.sra.ebi.ac.uk/vol1/fastq/SRR247/027/SRR24727827/SRR24727827_1.fastq.gz,SRR24727827_R1.fastq.gz
ftp://ftp.sra.ebi.ac.uk/vol1/fastq/SRR247/027/SRR24727827/SRR24727827_2.fastq.gz,SRR24727827_R2.fastq.gz
```

And then ran the script again with the code provided: `./download_sra.sh sra_downloads.txt`

**Results #2:**

It worked, both files were downloaded, renamed, and add to a downloads dir. As I wasn't sure what each section of the code was supposed to do, I asked another follow up question. 

**Question #3:** Can you explain each part of the download_sra.sh script and how it works?

**Results #3:**

Seemed to explain it pretty well, had a section for the file existence check and that `[! -f "$input_file"]` is for that, creating the directory, how the main download loop works with downloading and renaming the file, which it was able to do, and more. 

**Thoughts:**
It was very helpful, initially I was confused on why it only created the downloads file, but by allowing it to rewrite the `sra_downloads.txt` file, I was able to run it correctly. Interestingly, this wasn't the original code asking the question gave me, I had to restore the checkpoint to ask the question again after I thought I accidentally deleted a part of another script it gave me, so I think it is very interesting that it changed its answer. However, I think I may use this to download files for my final project. 