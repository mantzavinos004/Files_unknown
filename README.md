# Files_unknown
Guides for different file types







1) .ab = android backup
   1.dd if=<filename>.ab bs=24 skip=1 | zlib-flate -uncompress > <filename>.tar
   2. tar -xvf <filename>.tar
   3. Then you will get an /app and an /shared folder.
   4. there you fill find what you searching for
   5. TIP: to find in all the folders if there is something--> ls -a *

2) .sal = Signal Acquisition Log file???
   1) unzip <filename>.sal   ---> (gives two files: x.bin  with binary ifno and y.json with metadata)
   2) strings x.bin 
      a) you might find the <SALEAE> tag at the begin. then yu go to there website and download there debug tool. With          that you analyze the binaries and take the message 

3) .bin =binary
   1) strings <filename>.bin


4) .eml
   1) strings
  
5) 
