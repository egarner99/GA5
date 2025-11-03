
## Trial 1: 

**AI Tool** - GitHub Copilot

**Question 1:** How do I ignore files from a Git repository?

**Code Provided:**

It gave me a lot of different options that can be applied to several different situations (as seen in the screenshots), the one that I was looking for was how to ignore new/untracked files, in which it described creating a `.gitignore` file, type in the dirs and/or files you don't want tracked, then commiting the git ignore file:
 
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

The code it provided did work, and the answers seemed correct. It did give a lot of options, and although the explanations were good it was a bit overwhelming based on the short question I asked. However, this could just mean you have to be very specific with the questions. 


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

**Results 1:**

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

**Code Provided & Results:**: 

Using the one for Linux/macOS, it is a bit lengthy but can be found in the script `bulk-chmod.sh`. It also gave a tip to make it executable: `chmod +x bulk-chmod.sh`.

It also provided some examples, one of which I will be using to test: 
```bash
# Make all .sh files executable (keep other bits unchanged)
./bulk-chmod.sh --path ./scripts --match "*.sh" --files +x
```

I created new files to test this as well, `testfile.sh` and `testfile2.sh` and put them in a scripts dir.

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

After trying a couple of options based on the script, I asked another question as well:

**Question 3:** I entered in ./bulk-chmod.sh --path ./scripts --match "*.sh" --files +x to the terminal, why didn't it change the permissions?

**Code Provided & Results:** 

One option it gave was to try to add --recursive and --dry-run, which I tried: 
```bash
./bulk-chmod.sh --path ./scripts --files +x --recursive --dry-run
```

It also didn't work at first. I reloaded VS code and tried again, and got the output it said I should: 

```bash
Found 2 files and 1 directories to consider.
[DRY-RUN] chmod +x './scripts/testfile.sh'
[DRY-RUN] chmod +x './scripts/testfile2.sh'
Done.
```

Meaning that the original script works!

**Question 4/5:**

Can you explain for a 7th grader how the bulk-chmod.sh script works?

Can you explain in simple terms what the inside of the bulk-chmod.sh script does?

**Results 4/5:**

I prefer the explanation given for the second question, as it was a bit more in-depth (as seen in screenshots). It gave some code as well, but I had already tested the script.

**Thoughts:**

I thought that Microsoft Copilot was helpful, it gave pretty straightforward answers. Even though the issue was just that I needed to reload VS Code, if there was an issue with the original code it seems pretty good at trouble-shooting. The script's instructions were pretty clear with how to use it as well. My only complaint would be you have to create the .sh files and create the script manually, unlike GitHub Copilot. In regards to how it works, based on what the AI says (see screenshots for question 4/5), it confirms that a path and action were given, determines the file or dir that you want to change, and then changes the permission to what you want it to be, and with dry-run, it just states what it would do to the terminal, which it seemed to do. Though I didn't take screenshots of all of them, the code to do this on a Windows was also provided as an option. 


**Notes:**

I also went back and checked if the first code I entered, `./bulk-chmod.sh --path ./scripts --match "*.sh" --files +x` would work, and I added --dry-run at the end so it wouldn't change anything. It did (output below), so again the actual issue was that VS Code needed to reload. Nonetheless, Microsoft Copilot was pretty helpful!

Output: 
```bash
Found 2 files and 1 directories to consider.
[DRY-RUN] chmod +x './scripts/testfile2.sh'
[DRY-RUN] chmod +x './scripts/testfile.sh'
Done.
```

## Trial 3: 

**AI Tool:** GitHub Copilot

**Question 1:** Write code to analyze files using the program STAR. 

**Code Provided:**

It first created a `run_star.sh` script and asked for an allow to make it executable: 
```bash
chmod +x /fs/ess/PAS2880/users/egarner99/GA5/run_star.sh && echo 'chmod OK'
```

According to the AI, it did the same to create a test dir and test samples, as well as did a test dry-run I believe:

```bash
mkdir -p test_star_index test_star_fastq && cd test_star_fastq && touch sample_R1.fastq.gz sample_R2.fastq.gz sampleSE.fastq.gz && cd .. && ./run_star.sh -i test_star_index -p -t 4 -n test_star_fastq
```

The code in the script is a bit lengthy, and can be seen in `run_star.sh`. 

It also gave different codes to run it, the one I'm going to try is the dry-run: 
```bash
./run_star.sh -i /path/to/star_index -p -n -o star_results samples/*_R1.fastq.gz
```

**Results 1:**

After a bit of trial and error, the code does seem to work, using the dry run code: 
```bash
./run_star.sh -i test_star_index/ -p -n -o star_results test_star_fastq/*_R1.fastq.gz
```

I got the output: 
```bash
+ STAR --genomeDir test_star_index/ --readFilesIn /fs/ess/PAS2880/users/egarner99/GA5/test_star_fastq/sample_R1.fastq.gz /fs/ess/PAS2880/users/egarner99/GA5/test_star_fastq/sample_R2.fastq.gz --runThreadN 8 --outFileNamePrefix star_results/sample/ --outSAMtype BAM SortedByCoordinate --readFilesCommand zcat
Done (dry-run=1). Output base dir: star_results
```

**Question 2:** Can you explain in simple terms the inside of the run_star.sh script

**Results 2:**

It seemed to explain it pretty well, based on the AI (see screenshots for question 2), it confirms the files or dirs that you want, then creates a command for each file to then "send" to STAR. It also has options for a dry-run. 

It also gave some code to run, but again this has already been tested. 

**Thoughts:**
I really like the dry-run options, similar to Microsoft Copilot, giving me a chance to see if it works before attempting to actually run. I think its interesting that it will do a dry-run on its own before finishing its response to seemingly "test" its answer, but otherwise it is very informative. Using the dry-run option, the code worked as well. I may have to use this for my final project as well. 


## Trial 4: 

**AI Tool:** GitHub Copilot

**Question 1:** Write a script to run fastq.gz files through TrimGalore through apptainer.

**Code Provided:**
It created a script called `run_trimgalore.sh` (exact code can be seen in the script) and asked for permission to run this command: `chmod +x /fs/ess/PAS2880/users/egarner99/GA5/run_trimgalore_container.sh && echo "chmod OK"`

It also asked for permission to create test dirs and samples: 
`mkdir -p test_trim/data && cd test_trim/data && touch sample_R1.fastq.gz sample_R2.fastq.gz single.fastq.gz && cd ../.. && ./run_trimgalore_container.sh -n -p -o trimmed test_trim/data/*.fastq.gz`

It gave me a few options to use, the one I am going to try is:
```bash
./run_trimgalore_container.sh -c trim-galore.sif -p -o trimmed_output data/*.fastq.gz
```

It also gave me code to get the Trim Galore container:
```bash
apptainer pull trim-galore.sif docker://quay.io/biocontainers/trim-galore:0.6.7--hdfd78af_0
```

I opened the container using the code given, then using the code provided earlier I ran the script (the data dir just had some garrigos-data files I copied):
```bash
./run_trimgalore_container.sh -c trim-galore.sif -p -o trimmed_output data/*.fastq.gz
```

**Results 1:**

It looks like the code worked, it created a `trimmed_output` dir which contained `.fq.gz` files and `.fastq.gz_trimming_report.txt` for the two files I had in the data dir. It also created a trim-galore.sif filed, and printed quite a bit of text to the screen, the final of which said: 
```bash
Done (dry-run=0). Output directory: trimmed_output
```
The full output was put in a file called `trim_galore_trial` if needed for reference.

**Question 2:** Can you explain what this script does in simple terms?

**Results 2:**

Based and summarizing what the AI stated (see screenshots), it accepts the options given in the script, determines which fastq files to run based on the path given, makes an output dir, and collects pairs if they are there and creates a commamd for each file to run it through TrimGalore. Similar to the others, it also has a dry run option that will just says what it would do to screen.


**Thoughts:**

I liked how the AI created the script for me, unlike Microsoft CoPilot where you have to create and enter in the code manually. I also like how it provided different usage options, as well as described what the options in the code does. The script is a bit complicated, but based on what the AI says it is supposed to do (accept the files given, run each one through Trim Galore) it worked correctly. This is a bit different than Microsoft Copilot, which seems to give more simple answers.

## Trial 5 (extra):

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

**Result 1:**

The code didn't seem to really work, all it did was create the downloads dir. It looks like I missed a step, so I allowed it to create an example input file based on its suggestion.

**Question 2:** Yes, create an example input file with the urls ftp://ftp.sra.ebi.ac.uk/vol1/fastq/SRR247/027/SRR24727827/SRR24727827_1.fastq.gz
ftp://ftp.sra.ebi.ac.uk/vol1/fastq/SRR247/027/SRR24727827/SRR24727827_2.fastq.gz

**Code Provided:**
It changed my sra_downloads.txt file: 
```bash
ftp://ftp.sra.ebi.ac.uk/vol1/fastq/SRR247/027/SRR24727827/SRR24727827_1.fastq.gz,SRR24727827_R1.fastq.gz
ftp://ftp.sra.ebi.ac.uk/vol1/fastq/SRR247/027/SRR24727827/SRR24727827_2.fastq.gz,SRR24727827_R2.fastq.gz
```

And then ran the script again with the code provided: `./download_sra.sh sra_downloads.txt`

**Results 2:**

It worked, both files were downloaded, renamed, and add to a downloads dir. As I wasn't sure what each section of the code was supposed to do, I asked another follow up question. 

**Question 3:** Can you explain each part of the download_sra.sh script and how it works?

**Results 3:**

Seemed to explain it pretty well, to summarize what it said, the code checks if the file is present with `[! -f "$input_file"]`and creates a new directory. In the main section, the `while` begins the loop, the field separator becomes a comma (so that the file url and new name become two different variables), and then uses that to download and rename the files. It was able to do so. 

**Thoughts:**
It was very helpful, initially I was confused on why it only created the downloads file, but by allowing it to rewrite the `sra_downloads.txt` file, I was able to run it correctly. Interestingly, this wasn't the original code asking the question gave me, I had to restore the checkpoint to ask the question again after I thought I accidentally deleted a part of another script it gave me, so I think it is very interesting that it changed its answer. However, I think I may use this to download files for my final project.


## Note: 
I tried to organize most of the example/test files based on the trials they were used in, though a few may be mixed up!

Committed to the git repository GA5