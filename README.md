# Files_unknown
Guides for different file types

try this first:

strings <filename> | grep "password="

strings <filename> | grep PWD




1) .ab = android backup
   1.dd if=<filename>.ab bs=24 skip=1 | zlib-flate -uncompress > <filename>.tar
   
   2. tar -xvf <filename>.tar
  
   4. Then you will get an /app and an /shared folder.
      
   6. there you fill find what you searching for
      
   8. TIP: to find in all the folders if there is something--> ls -a *
---------------------------------------------------------------------------------------------------------------------------
2) .sal = Signal Acquisition Log file???
   
   1) unzip <filename>.sal   ---> (gives two files: x.bin  with binary ifno and y.json with metadata)
      
   3) strings x.bin 
      a) you might find the <SALEAE> tag at the begin. then yu go to there website and download there debug tool. With          that you analyze the binaries and take the message 
---------------------------------------------------------------------------------------------------------------------------
3) .bin =binary
   
   1) strings <filename>.bin
----------------------------------------------------------------------------------------------------------------------------

4) .eml
   
   1) strings
----------------------------------------------------------------------------------------------------------------------  
5) .mid
   
   1) First, we'll check the file with hidden messages in 'Program Change': https://github.com/maxcruz/stegano_midi
      if gives base64, then decrypt it
      
   3) try it in the audacity app
      
   if those are normal try this script  for DAW:
   
import mido

from collections import Counter


midi_filename = "final_version_v199237.mid"

mid = mido.MidiFile(midi_filename)

notes = []

for track in mid.tracks:

    for msg in track:
        if msg.type == 'note_on' and msg.velocity > 0:
            notes.append((msg.note, msg.velocity))

velocity_counts = Counter(velocity for _, velocity in notes)


if velocity_counts:

    most_common_velocity, count = velocity_counts.most_common(1)[0]
    print(f"Most common velocity: {most_common_velocity} ({count} times)")

filtered_velocity = [];

for note, velocity in notes:

    if velocity != most_common_velocity:
        filtered_velocity.append(velocity)
print("Filtered velocities:")

print(filtered_velocity)


and then :

flag = ''.join(chr(code) for code in filtered_velocity)

print("Flag:")

print(flag)
------------------------------------------------------------------------------------------------------------------------------
6) mp4 files/videos

Tools like https://y2down.cc/ can help downloading the MP4 file containing the video.
then use ffmpeg

$fmpeg -i teaser.mp4 -vf "fps=1" frames/out%04d.png

Well, the number of frames is huge. Over 1600 pictures. Too much to look at, but we can use another tool - OCR named tesseract

$ for file in frames/*.png; do tesseract "$file" stdout >> results.txt; done

It takes a moment, but after a while we got results.txt file we can check. It contains a bunch of crap, but using grep we can get our flag:

$ cat results.txt | grep 1753c{
------------------------------------------------------------------------------------------------------------------------------

7) .kdbx
   
   you need keepass to find the code.
   
   sudo apt install keepassxc
   
   git clone keepass4brute.sh
   
   and run it with rockyou.txt

---------------------------------------------------------------------------------------------------------------------------
8) .doc

You need oletools:

pip install -U oletools --break-system-packages

then: 

a. oleid filename.doc

b. 
---------------------------------------------------------------------------------------------------------------------------
9) .elf
    
   1.   vol -f name.elf windows.pslist            (gives running processes on the machine, search for weird names.exe and keep there PID)
  
   2.   vol -f name.elf windows.netscan            (gives connections at the time of dump taken, try to find the samw weird .exes running)
  
   3.   vol -f name.elf windows.cmdline            (get commands that were used to run those processes)

  or

   4.   vol -f name.elf windows.cmdline --pid 1234
    








