# Chapter Tenth: Appendix - Bash commands

You might need the following commands. 

This allows you to execute script files or change the content of a file with shell:
```
chmod u+x name_of_file
```
```chmod``` means change mode (make it executable), ```u``` means for all users and ```x``` means executable (```+``` is the liaison key word).

To change the content of a file use ```sed```:
```
sed -i {line_number}s/*/text_to_replace name_of_file
```

```-i``` means it will safe the file with the modifications. 

