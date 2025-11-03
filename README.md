
## Trial 1: 

**AI Tool** - GitHub Copilot

**Question 1:** How do I ignore files from a Git repository?

**Code Provided:**

It gave me a lot of different code that can be applied to several different situations (as seen in the screenshots), the one that I was looking for was how to ignore new/untracked files, in which it described creating a `.gitignore` file and typing in the dirs and/or files you don't want tracked, then commiting the git ignore file:
 
```bash
git add .gitignore
git commit -m "Add .gitignore"
```

Another that I thought was interesting was to stop tracking files that are already committed; it provided two options for single and multiple files: 

Single files: 
```bash
git rm --cached path/to/file.fastq.gz
git commit -m "Stop tracking large fastq"
```

Multiple files: 
```bash
git rm -r --cached .
git add .
git commit -m "Apply .gitignore to repository"
```

**Results #1:**
Since I already had a .gitignore file, I followed the code provided to commit it, which worked. 
Output: 
```bash
git commit -m "Add .gitignore"
[main 2652530] Add .gitignore
 1 file changed, 3 insertions(+)
 create mode 100644 .gitignore
```

I also tried the single file command to stop tracking files that are already commited. I created a test file for this, and commited it: 
```bash
touch testfile.md
add testfile.md
git add testfile.md
git commit -m "For Trial 1"
```

I then used the command and changed it for the file: 
```bash
git rm --cached testfile.md
git commit -m "Stopped tracking"
```

And got the output:
```bash
[main 5844101] Stopped tracking
 1 file changed, 0 insertions(+), 0 deletions(-)
 delete mode 100644 testfile.md
```

Checking git status also showed it was now untracked as well. 

**Thoughts:** 

The code it provided did work, and the answers did seem work. It did give a lot of options though, and although the explanations were good, it was a bit overwhelming based on the question I asked. This could just mean you have to be very specific with the questions. 


## Trial 2: 

**AI Tool:** Microsoft Copilot

**Question 1:** How do I change permissions on a file in VS Code?

**Code Provided:** 

Based on the outputs (as seen in screenshots), the command to use is: 

```bash
chmod 644 filename.txt    # Read/write for owner, read-only for others
chmod +x script.sh        # Make a script executable
```

And to check permissions: 
```bash
ls -l filename.txt
```

**Results #1:**

I tried the check permissions command initially, and got the output: 

```bash
-rw-rw----+ 1 egarner99 PAS2880 0 Nov  2 19:42 testfile.md
```

I tried `chmod 644 testfile.md`, and it actually worked: 

```bash
-rw-r--r--+ 1 egarner99 PAS2880 0 Nov  2 19:42 testfile.md
```

I tested the other as well to make it executable, and it worked as well:
```bash
-rwxr-xr-x+ 1 egarner99 PAS2880 0 Nov  2 19:42 testfile.md
```


**Question 2:** One option it offered was to create a script that sets permissions for multiple files automatically, so I asked it to do so: Yes, create a script that sets permissions for multiple files automatically. 

**Code Provided**: 

Using the one for Linux/macOS, it is a bit lengthy but can be found in the script `bulk-chmod.sh`. It also gave a tip to make it executable: `chmod +x bulk-chmod.sh`.

It also provided some examples, one of which I will be using to test: 
```bash

# Make all .sh files executable (keep other bits unchanged)
./bulk-chmod.sh --path ./scripts --match "*.sh" --files +x
```

I created a new files to test this as well, testfile.sh and testfile2.sh and put them in a scripts dir.

I then ran the code as follows:
```bash
 ./bulk-chmod.sh --path ./scripts --match "*.sh" --files +x
```

Unfortunately, it didn't work: 
```bash
total 0
-rw-rw----+ 1 egarner99 PAS2880 0 Nov  2 20:20 testfile2.sh
-rw-rw----+ 1 egarner99 PAS2880 0 Nov  2 20:19 testfile.sh
```

Looking at the script and also based 







**Thoughts:**

This question was a bit simple, but I like how straightforward the answers was, and how it gave different options for both Linux/MacOS and Windows. 





















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

Seemed to explain it pretty well, had a section for the file existence check and that `[! -f "$input_file"]` is for that, creating the directory, how the main download loop works with downloading and renaming the file, which it was able to do, and more (as seen in the screenshots). 

**Thoughts:**
It was very helpful, initially I was confused on why it only created the downloads file, but by allowing it to rewrite the `sra_downloads.txt` file, I was able to run it correctly. Interestingly, this wasn't the original code asking the question gave me, I had to restore the checkpoint to ask the question again after I thought I accidentally deleted a part of another script it gave me, so I think it is very interesting that it changed its answer. However, I think I may use this to download files for my final project. 