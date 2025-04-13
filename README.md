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
  
5) .mid
   1) First, we'll check the file with hidden messages in 'Program Change': https://github.com/maxcruz/stegano_midi
      if gives base64, then decrypt it
   2) try it in the audacity app
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



