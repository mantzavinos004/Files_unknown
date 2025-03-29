# Files_unknown
Guides for different file types







1) .ab = android backup
   1.dd if=<filename>.ab bs=24 skip=1 | zlib-flate -uncompress > <filename>.tar
   2. tar -xvf <filename>.tar
   3. Then you will get an /app and an /shared folder.
   4. there you fill find what you searching for
   5. TIP: to find in all the folders if there is something--> ls -a *
