# Appendix: Bash

Bash is a scripting langauge, used on Unix machines. You might need the following commands.

## Make a bash file executable

This allows you to execute script files or change the content of a file with shell:

```bash
chmod u+x name_of_file.sh
```

`chmod` means change mode (make it executable), `u` means for all users and `x` means executable (`+` is the liaison key word).

You can then run the script by typing `./nameoffile.sh`.

## Some bash commands

To change the content of a file use `sed`:

```bash
sed -i '143s/*/text_to_put_on_the_line' name_of_file
```

`sed` stands for stream editor. `-i` means it will save the file with the modifications. `-s` is for substitution. This will act on line 143 only.

You can also substitute a word (snetence) with another sentence

```bash
sed 's/sentenceToChange/newSentence/g' myfile.txt
```

Stream editor is a convenient tool that can be used for other tasks. For example, filtering lines of a text file (and copying them into another text files).

```bash
sed -n '1p' textfile.txt > textfile2.txt
```

\-n stands for filtering and the p after the 1 for print. To copy only even lines, do

```bash
sed -n '2~2p' textfile.txt > textfile2.txt
```

The '2\~2' means start at line two and keep every line by step of 2. TO keep lines 5 to 10 you can use '5,10p'. To keep several diferent ranges of lines (line 1 to 10 and line 21 to 30) use

```bash
sed -n -e '1,10p' -e '21,30p' textfile.txt > textfile2.txt
```

## commands

Adding the symbol `&` at the end of a line will have the job run in the background, so the script will continue to the next line. It is a convenient way to launch several jobs on a cluster, for example. ``&#x20;
