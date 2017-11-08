Read and write on files

To read or write on a file in Fortran one must first _open_ it. To open a file name mytextfile.txt one can write

open\(unit=10, file="mytextfile.txt", status = new/old, action = read/write\)

Only the first two argument \(unit and file\) are mandatory. You can choose any integer for unit \(it can also be a variable integer\), as long as it is not used by another file \(for example mytextfile\_2.txt\).

After working on the file, you need to close it with the command

close\(10\)

Reading

Fortran will read line by line, so if your file is a data file with one observation per line and 5 variables, say, you can get this data into a matrix in the following way

do j=1, 15  
read\(10,\*\) var1\(j\) var2\(j\) var3\(j\) var4\(j\) var5\(j\)  
end do

To write in a file, if you have a matrix with N lines with an identifier and a result \(scalar\) you can write

do j=1,N  
write\(10,\*\) \(matresult\(j,i \),i=1,2\)  
end do





