# Chapter Tenth: Appendix - Bash commands

Bash is a scripting langauge, used on Unix machines. You might need the following commands.

This allows you to execute script files or change the content of a file with shell:

```bash
chmod u+x name_of_file.sh
```

`chmod` means change mode \(make it executable\), `u` means for all users and `x` means executable \(`+` is the liaison key word\).

You can then run the script by typing `./nameoffile.sh`.

To change the content of a file use `sed`:

```bash
sed -i {line_number}s/*/text_to_put_on_the_line name_of_file
```

`sed` stands for stream editor.  `-i` means it will save the file with the modifications.

