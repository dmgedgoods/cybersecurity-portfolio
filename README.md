# cybersecurity-portfolio
### NSA Codebreakers Challenege 

Welcome to my Codebreakers 2025 retrospective. I wanted to do this challenege to see how far I could go, and I didn't go far. However I learned more than I have learned in any other CTF I have ever attempted. 

I have had an interest in all thing security and cyber since I was a young kid. This was a chance for me to see how much I actually know. Applying my basic skills to this challenge was not enough. I had to truly think outside the box and even that only got me so far. The technicality and difficulty of each challenege can be understated. I spent WEEKS working on one problem. 

In all of this difficulty, I had moments of clarity and completion that I am proud of. This grind served as a solid reality check on my reliance on GUI-based forensics. Wireshark is great for visualization, but when you are dealing with traffic that doesn't play by standard protocol rules, or when the extraction plugins simply fail to recognize the artifact, you can't just stare at the screen waiting for a parser to save you. This challenge forced me to get uncomfortable with tshark and tcpdump, moving away from "point-and-click" analysis to building custom filters that hunt for behavior rather than just signatures.

The biggest takeaway was discovering the value of the "nuclear option": ignoring protocol headers entirely and analyzing raw payload. There were moments where the automated parsers were blind to the data I needed because of control channel stuff. By dropping down to raw dumps with tcpdump and straightforward grep patterns, I bypassed the tool's logic and went straight to the source. It reinforced that while tools are force multipliers, knowing how to manually carve data from the wire is the only fallback that matters when the automation breaks.

Here is a shortlist of some of my favorite commands that I keep in my book:

tcpdump -r traffic.pcap -A -n	
    Reads the pcap (-r), prints payloads in ASCII (-A), and skips DNS resolution (-n).

tcpdump ... link-type LINUX_SLL2	
    You'll see this warning for Cooked Captures. It means "Ignore MAC headers, look at payloads."

tshark -r traffic.pcap -q -z io,phs	
    Protocol Hierarchy. Shows which protocols (TCP, UDP, HTTP, FTP) are present by percentage.

tshark -r traffic.pcap -q -z conv,ip	
    Conversations. Lists all IP-to-IP conversations, sorted by volume. Good for spotting top talkers.

tshark -Y 'frame contains "pass"'	
    Deep Search. Filters for any packet containing the string "pass" in the payload.

tshark ... -T fields -e ip.src -e tcp.stream	
    Field Extraction. Prints only the specific columns you want (Source IP, Stream ID).

tshark ... --export-objects ftp-data,output_dir	
    File Carving. Attempts to automatically extract files from a specific protocol (ftp-data, http, tftp).

This was an eye opening experience for me and I look forward to participating again later this year. I encourage everybody who has even the smallest interest in cybersecurity to participate. It is worth more than you can imagine. 
