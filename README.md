“Task 5: Capturing and Analyzing Network Traffic with Wireshark”

What I Actually Did 📋
I’ll be honest — I was a little intimidated opening Wireshark for the first time. It felt like staring into the Matrix… lines of raw packets just flooding the screen, and I had no idea what I was looking at.

But then I remembered something my mentor (the legendary ghost with 199.99 years of experience) told me:

"Packets don’t lie. They whisper secrets — if you learn how to listen."

So I fired up Wireshark, picked my active interface, and just let it run for about a minute while I browsed example.com, pinged google.com, and opened a few tabs to generate traffic.

At first, it was chaos. But slowly… patterns started forming. And I started seeing the web for what it really is — a constantly buzzing swarm of protocols all talking beneath the surface.

My Setup ⚙️
OS: Kali Linux 2023.4 (running in VirtualBox on Windows 11)

Wireshark Version: 4.2.3

Capture Duration: ~60 seconds

Interface Used: eth0 (virtual bridged adapter)

Traffic Generators:

ping google.com

Browsed example.com, wikipedia.org

Let a few apps run silently in background

Saved the .pcapng file and made sure to tag the key protocol filters while capturing.

What I Discovered 🔍
I identified four main protocols during my session:

1. DNS (Port 53)
This was the first thing that stood out — every time I visited a site, there was a DNS query firing off first.
I noticed A record lookups for example.com, wikipedia.org, and even some domains I never typed.
That’s when it clicked: apps in the background constantly resolve hostnames. Wild.

2. HTTP (Port 80)
When I hit example.com, I could actually see the GET request and the server's HTTP/1.1 200 OK response.
I followed the TCP stream and was shocked — full request headers, plain-text content… all right there.
Felt both powerful and a little scary.

3. TCP (Various Ports)
I tracked a couple of three-way handshakes (SYN → SYN/ACK → ACK) and finally understood how a connection starts.
Even watched a couple of sessions gracefully terminate (FIN → ACK).
These patterns were everywhere, and now I know what to look for.

4. ARP (Broadcast)
ARP packets were resolving MAC addresses constantly.
I didn’t even touch anything on the network — yet these little broadcasts kept saying “Who has 192.168.0.1? Tell 192.168.0.100.”
That blew my mind. My system was talking — even when I wasn’t.

Surprises & Weird Stuff 🤔
Background DNS queries were the biggest shock. I wasn’t browsing, yet names like ocsp.digicert.com and telemetry.mozilla.org were being resolved.

Captured a couple of TLS handshakes when I visited HTTPS sites, but couldn’t see the payload — which actually felt reassuring (encryption works).

Noticed some traffic from ntp — the system syncing time in the background. Never thought about that before.

A few packets were labeled “Malformed.” I’m still not sure what that means — maybe retry attempts?

What This Taught Me 🧠
This task was a reality check.
Until now, “the internet” was just browser tabs and apps.
But Wireshark showed me the actual conversations — raw, silent, constant.

Here’s what clicked for me:

Every action — typing a URL, opening an app — triggers multiple protocol layers I never saw before.

Privacy is complicated. Even if content is encrypted (HTTPS), metadata leaks still happen (like domain names, IPs, ports).

My system does a lot on its own. Even without input, it's reaching out — updating time, checking certificates, sending telemetry.

Security isn’t just about blocking malware — it’s about understanding behavior at this level.
This task made me feel like I’m finally looking at traffic like a real analyst.

Evidence Package 📎
task5_capture.pcapng — raw packet data

dns_filter_view.png — filtered DNS traffic

tcp_handshake_follow_stream.png — TCP connection analysis

http_get_request.png — full HTTP session capture

protocol_hierarchy_stats.png — auto breakdown of all protocols

Personal Takeaway 💭
“Wireshark didn’t just show me packets — it showed me how loud quiet systems really are.”

I’m still learning, still confused at times, but this task flipped a switch in my brain.
Now when someone says “the network is acting weird,” I don’t feel helpless — I feel curious.
And that’s the difference between using tools… and becoming an analyst.