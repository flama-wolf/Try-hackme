  https://tryhackme.com/room/sakura?utm_campaign=social_share&utm_medium=social&utm_content=room&utm_source=copy&sharerId=66e82296fadc2618b6619837

# **Chronological Forensic Analysis and OSINT Investigation of the Sakura Room Incident**

## **Investigative Framework and Incident Overview**

The digital forensic landscape is often characterized by the meticulous reconstruction of events following a security breach. In the case of the OSINT Dojo, the investigation was triggered not by a massive data exfiltration or a ransomware payload, but by a singular, taunting artifact: a Scalable Vector Graphics (SVG) image left behind by a threat actor.1 This report details the exhaustive investigative journey undertaken to de-anonymize the individual responsible, tracing their digital footprint across various platforms, financial ledgers, and physical geographic locations. The methodology employed follows the classic OSINT lifecycle: collection, processing, exploitation, production, and dissemination.

The investigation leverages a variety of specialized techniques, ranging from metadata extraction and cryptographic analysis to blockchain forensics and geospatial intelligence.2 Each phase of the journey reveals a fundamental failure in the attacker's operational security (OPSEC), demonstrating how a single unique identifier—in this case, a consistent username—can serve as the linchpin for a total identity compromise.2 The transition from a digital handle to a physical residence in Japan highlights the power of passive reconnaissance when executed with precision and a deep understanding of the tools available to the modern investigator.

## **Phase I: Artifact Analysis and Initial Lead Generation**

The investigation commenced with the forensic examination of the image file titled "sakurapwnedletter.svg".1 Unlike standard raster formats like JPEG or PNG, which store data as a grid of pixels, SVG files are XML-based vector images. This distinction is critical for investigators because SVG files contain human-readable source code that can be inspected for hidden comments, embedded scripts, or anomalous data structures.3

### **Visual Deconstruction and Binary Decoding**

Upon initial viewing, the image displayed a distinctive aesthetic: a pink background with binary code, overlaid with a message stating "You've been pwned".5 The presence of binary in a high-contrast format suggested that the attacker intended for it to be found, functioning as a deliberate breadcrumb or a technical gate. The analyst utilized the "Inspect Element" tool within a browser environment to access the Document Object Model (DOM) of the SVG, allowing for the direct extraction of the binary strings without the need for manual transcription.3

The extraction revealed a series of binary blobs which, when processed through a binary-to-text converter, yielded a specific instruction: "Check the metadata".3 This finding confirmed that the binary was a standard ASCII encoding of a plain-text hint, moving the investigation from visual analysis to the underlying file structure.

### **Metadata Extraction and the Primary Handle**

Following the hint found in the binary code, the investigation focused on the Exchangeable Image File Format (EXIF) and other metadata embedded within the SVG file. Metadata is often overlooked by novice threat actors, yet it frequently contains information regarding the software used, the time of creation, and, most crucially, the file paths from the creator's local system.2

Using a command-line utility such as exiftool or a web-based metadata viewer, the analyst inspected the internal fields of the file.1 A specific field, Export-filename, provided the breakthrough needed to move the investigation forward. This field contained a directory path that revealed the attacker's system username: **SakuraSnowAngelAiko**.1

| Metadata Field | Extracted Data | Analytical Significance |
| :---- | :---- | :---- |
| File Format | SVG (Scalable Vector Graphics) | XML-based, allows for source code inspection.1 |
| Visual Hint | Binary String in Backdrop | "Check the metadata" \- Instructional lead.6 |
| Export-filename | /home/sakurasnowangelaiko/Desktop/... | Revealed the primary investigative pivot point.1 |
| Software | Inkscape | Indicates the tool used for graphic design.2 |

The discovery of a highly unique and specific handle allowed the investigator to pivot from the initial artifact to broad-spectrum reconnaissance across the surface web.2

## **Phase II: Digital Footprint Expansion and Identity Correlation**

The second phase of the investigation focused on Social Media Intelligence (SOCMINT). The goal was to determine if the handle SakuraSnowAngelAiko was reused across other platforms, a common practice among users who develop an emotional or professional attachment to a specific digital identity.2

### **Platform Cross-Referencing**

A comprehensive search of the handle across various platforms yielded immediate and high-confidence results. The attacker had established a presence on X (formerly Twitter), GitHub, and LinkedIn.3 The presence of a LinkedIn account was particularly notable, as it suggested the attacker might be maintaining a professional persona alongside their more clandestine activities.4

| Platform | Profile Findings | Information Gained |
| :---- | :---- | :---- |
| GitHub | Active repositories including "PGP" and "ETH" | Technical interests, crypto wallets, PGP keys.6 |
| X (Twitter) | Introduction posts and travel photography | Real name, travel history, taunting behavior.3 |
| LinkedIn | Educational and work history | Potential confirmation of real-world identity.4 |

By analyzing the X profile, the investigator located an introductory post where the attacker explicitly shared their real name: **Aiko Abe**.6 This transition from a pseudonym to a legal name represented a significant escalation in the de-anonymization process, providing a concrete target for further background research.

### **Cryptographic Identity Extraction**

The GitHub account provided a more technical look into Aiko Abe's identity. A repository titled "PGP" contained a public PGP key.6 PGP (Pretty Good Privacy) keys are used for secure communication, but the metadata associated with a public key often includes a User ID (UID) string, which typically contains the owner's name and email address.7

The analyst exported the public key content into a .asc file and used the gpg \--show-keys command to inspect the metadata.7 The extraction successfully revealed the attacker's primary contact email: **SakuraSnowAngel83@protonmail.com**.6 The use of ProtonMail, a Switzerland-based encrypted email service, indicates that while the attacker was conscious of privacy, their failure to scrub the key's metadata undermined their choice of a secure platform.6

## **Phase III: Blockchain Forensics and Financial Intelligence**

With a technical profile established, the investigation shifted toward Financial Intelligence (FININT) by exploring the "ETH" repository found on the attacker's GitHub.6 The repository's name served as a clear indicator of the attacker's involvement with the Ethereum blockchain.

### **Recovery of the Ethereum Wallet**

Blockchain forensics relies on the immutable and transparent nature of distributed ledgers. While the attacker might have attempted to hide their current activities, the Git version control system maintains a history of all changes made to a repository.1 By auditing the commit history of the "ETH" repository, the investigator found an earlier version of a file that had been subsequently modified or deleted. This original commit contained the attacker's Ethereum wallet address: **0xa102397dbeeBeFD8cD2F73A89122fCdB53abB6ef**.1

### **Transactional Audit via Etherscan**

The wallet address was then queried on Etherscan, a popular blockchain explorer. The transaction history of the wallet provided a window into the attacker's economic behavior during the period of January 2021\.5

| Financial Metric | Data Points | Significance |
| :---- | :---- | :---- |
| Primary Asset | Ethereum (ETH) | Primary currency for mining and transactions.6 |
| Mining Pool | Ethermine | Identified via incoming payments on Jan 23, 2021\.1 |
| Transaction History | Interaction with Tether (USDT) | Indicates asset diversification or stablecoin conversion.6 |
| Wallet Address | 0xa102397dbeeBeFD... | Persistent identifier for financial tracking.1 |

The audit revealed that Aiko Abe was receiving consistent payouts from **Ethermine**, a well-known mining pool.1 This detail suggests that the attacker possessed the technical hardware and knowledge necessary for cryptocurrency mining. Furthermore, the records showed transactions involving **Tether (USDT)**, which is often used by traders to hedge against the volatility of Ethereum or to prepare for fiat off-ramping.6

## **Phase IV: Dark Web Reconnaissance and Network Intelligence**

As the investigation continued, the attacker moved to a new X handle, **@SakuraLoverAiko**, from which they continued to taunt the OSINT Dojo.6 This handle change was likely an attempt to reset their digital footprint, but the previous findings had already linked the two accounts through behavioral patterns and shared interests.9

### **The Onion Link and DeepPaste Analysis**

A tweet from the new account contained cryptic references to "DEEP" and "PASTE," as well as a mention of "Regular WiFi and Passwords".4 The investigator interpreted these as clues pointing toward a dark web pastebin service hosted on the Tor network. Onion services are frequently used for sharing sensitive or illicit data because they provide anonymity for both the host and the visitor.7

Using the Tor Browser, the analyst navigated to a specific Onion URL identified through the attacker's hints: http://deepv2w7p33xa4pwxzwi2ps4j62gfxpyp44ezjbmpttxz3owlsp4ljid.onion.7 This "DeepPaste" service contained a post authored by the attacker that included the Service Set Identifier (SSID) for their home WiFi network: **DK1F-G**.6

### **Signal Intelligence via WiGLE**

While an SSID is merely a name, it can be mapped to a physical location using the Wireless Geographic Logging Engine (WiGLE). WiGLE is a database of wireless networks that have been "wardriven" or mapped by contributors worldwide.6 By performing an advanced search for the SSID "DK1F-G," the investigator was able to retrieve the Basic Service Set Identifier (BSSID), which is the MAC address of the wireless access point.6

| Network Parameter | Value | Functional Role |
| :---- | :---- | :---- |
| SSID | DK1F-G | Human-readable network name used for search.6 |
| BSSID | 84:AF:EC:34:FC:F8 | Unique hardware address of the router.6 |
| Geographic Region | Japan | Narrowed the search to the attacker's home country.6 |
| Specific City | Hirosaki | Final physical location of the network.5 |

The mapping of the BSSID to a specific set of coordinates in **Hirosaki, Japan**, provided the first definitive link between the attacker's digital persona and a physical residence.5

## **Phase V: Geospatial Intelligence and the Journey Home**

The final phase of the investigation, known as "Homebound," involved tracking the attacker's physical travel back to Japan using photos and maps shared on social media.1 This required a synthesis of Image Intelligence (IMINT) and Geographic Information Systems (GIS) techniques.

### **Departure from Washington, D.C.**

The attacker shared a photo of cherry blossoms with a large, white obelisk in the background.6 Using visual search tools and landmark identification, the investigator determined the following:

1. **Landmark**: The obelisk was identified as the **Washington Monument** in Washington, D.C..6  
2. **Environmental Context**: The presence of **Okame** cherry blossoms confirmed the location and the time of year.6  
3. **Logistics**: The closest airport to this location, frequently used for international travel from the U.S. capital, is **Ronald Reagan Washington National Airport (DCA)**.5

### **The Layover: Haneda Airport**

A subsequent post from the attacker featured an image of a lounge area.3 The branding in the photo was identified as the **Sakura Lounge**, a premium lounge service operated by **Japan Airlines (JAL)**.3 By comparing the architectural details and the specific placement of the lounge's logo with known JAL lounge locations, the investigator narrowed the site down to **Tokyo Haneda Airport (HND)**.3 This indicated a common international layover pattern for travelers returning to regional Japanese cities from the United States.

### **Final Approach: Lake Inawashiro and Hirosaki**

As the attacker boarded their final flight home, they shared a map from their in-flight entertainment system or a GPS tracking app.3 The map displayed a large, heart-shaped lake. Cross-referencing this with satellite imagery of Japan allowed the analyst to identify **Lake Inawashiro** in the Fukushima Prefecture.3

Following the flight path further north, the investigation culminated in the city of **Hirosaki**.5 This city was already identified as the location of the attacker's WiFi network via the WiGLE database, confirming that Aiko Abe had completed her journey and returned to her home city.5

| Travel Waypoint | Identifier/Location | Supporting Evidence |
| :---- | :---- | :---- |
| Origin Airport | DCA (Reagan National) | Proximity to Washington Monument and Okame blossoms.5 |
| Layover Airport | HND (Haneda) | JAL Sakura Lounge branding and lounge layout.3 |
| In-Flight View | Lake Inawashiro | Distinctive shape of the lake on the shared map.6 |
| Final Destination | Hirosaki | Correlation between WiGLE BSSID and travel path.5 |

## **Behavioral Analysis and Attacker Profile**

The totality of the evidence allows for the construction of a detailed profile of the attacker, Aiko Abe. She is a technically proficient individual with a strong interest in graphic design (evidenced by the use of Inkscape and SVGs), cryptocurrency mining (evidenced by the Ethermine payments), and cyber-offensive techniques.1

Her psychology appears to be driven by a desire for recognition, as evidenced by the deliberate clues left in the binary code and her continued taunting of the OSINT Dojo on Twitter.4 However, her operational security was undermined by the classic mistake of identity consolidation—reusing the same handle and failing to separate her personal life (travel photos, LinkedIn) from her technical/offensive activities.2

## **Synthesis of Investigative Tools and Resources**

The success of this investigation was not due to any single tool but rather the creative orchestration of multiple OSINT resources. The following table provides an inventory of the toolset used throughout the journey.

| Tool Category | Specific Tool Used | Purpose in Investigation |
| :---- | :---- | :---- |
| Metadata Extraction | exiftool, ezgif.com | Revealed the local username in the SVG file.1 |
| Browser Forensics | Chrome/Firefox Inspect Tool | Extracted binary strings from the SVG source.3 |
| Data Conversion | RapidTables Binary-to-Text | Decoded hints hidden in the image background.3 |
| SOCMINT | Google, LinkedIn, X, GitHub | Linked handles to real names and email addresses.2 |
| Crypto Forensics | Etherscan.io | Traced transactions, wallets, and mining pools.5 |
| Dark Web Access | Tor Browser | Accessed DeepPaste to retrieve WiFi SSIDs.6 |
| Signal Intelligence | WiGLE.net | Mapped SSIDs to BSSIDs and physical locations.6 |
| Visual Geolocation | Google Lens, Google Earth | Identified monuments, blossoms, and flight paths.6 |

## **Conclusion and Strategic Takeaways**

The de-anonymization of Aiko Abe serves as a powerful case study for OSINT practitioners and cybersecurity professionals alike. It demonstrates that the digital world is far less anonymous than it appears to those who do not strictly adhere to the principles of compartmentalization. By starting with a single SVG file, the investigator was able to weave together a narrative that spanned multiple social media platforms, the Ethereum blockchain, the dark web, and several international airports, eventually arriving at the attacker's doorstep in Hirosaki, Japan.5

The investigation highlights several critical lessons for both defenders and researchers:

1. **Metadata is a Permanent Record**: Information embedded in files (like SVG source code or PGP metadata) persists long after the creator has forgotten about it.1  
2. **Blockchain is Public Ledger**: Every transaction is an immutable piece of evidence that can be traced back to mining pools and exchanges.1  
3. **Unique Identifiers are Vulnerabilities**: A unique username is a "primary key" that can be used to join disparate datasets across the internet.2  
4. **Geolocation is Multi-Faceted**: Physical location can be derived from visual landmarks, botanical evidence, and the signal intelligence of wireless networks.1

Through the diligent application of these OSINT techniques, the "journey through the Sakura Room" transforms from a simple CTF challenge into a comprehensive demonstration of modern digital investigative capabilities.1

## **Resources Used**

| Resource Name | Description / Use Case |
| :---- | :---- |
| TryHackMe Sakura Room | The original CTF environment providing the "sakurapwnedletter.svg" and initial prompts.2 |
| OSINT Dojo | The creators of the room and the fictional target of the cyberattack.1 |
| Exiftool | Essential command-line utility for metadata extraction.1 |
| Etherscan | Blockchain explorer for Ethereum transaction and wallet analysis.5 |
| WiGLE | Database for mapping wireless network identifiers to geographic coordinates.6 |
| Google Lens | Visual search engine used for landmark and blossom identification.6 |
| Tor Project | Infrastructure for accessing onion services and the DeepPaste link.7 |
| JAL Website | Research source for identifying Sakura Lounge locations and flight hubs.5 |
| GitHub Version History | Tool for auditing commit history to find deleted wallet addresses.1 |
| PGP/GPG Tools | Software for inspecting public keys and extracting user identity data.1 |
| Google Maps/Earth | GIS platforms for identifying Lake Inawashiro and city layouts.3 |

#### **Sources des citations**

1. TryHackMe: Sakura Room Complete Walkthrough \- Jasper Alblas, consulté le janvier 4, 2026, [https://www.jalblas.com/blog/tryhackme-sakura-room-walkthrough/](https://www.jalblas.com/blog/tryhackme-sakura-room-walkthrough/)  
2. Sakura Room \- TryHackMe, consulté le janvier 4, 2026, [https://tryhackme.com/room/sakura](https://tryhackme.com/room/sakura)  
3. TryHackMe | Sakura Room Writeup \- Carson Shaffer, consulté le janvier 4, 2026, [https://blog.carsonshaffer.me/tryhackme-sakura-room-9bd383654f7e](https://blog.carsonshaffer.me/tryhackme-sakura-room-9bd383654f7e)  
4. a3r0id/TryHackMe-Sakura-Room-Writeup \- GitHub, consulté le janvier 4, 2026, [https://github.com/a3r0id/TryHackMe-Sakura-Room-Writeup](https://github.com/a3r0id/TryHackMe-Sakura-Room-Writeup)  
5. TryHackMe — The Sakura Room. SPOILERS: If you haven ... \- Medium, consulté le janvier 4, 2026, [https://medium.com/@mathewbevans/tryhackme-the-sakura-room-091e4218967b](https://medium.com/@mathewbevans/tryhackme-the-sakura-room-091e4218967b)  
6. SAKURA ROOM \-TRY HACK ME- ROOM. Hello everyone\! This is a ..., consulté le janvier 4, 2026, [https://systemweakness.com/sakura-room-try-hack-me-room-21c07011a1e6](https://systemweakness.com/sakura-room-try-hack-me-room-21c07011a1e6)  
7. Sakura Room — TryHackme Challanges (Easy) \#2 | by Sibercat Media \- OSINT Ambition, consulté le janvier 4, 2026, [https://publication.osintambition.org/osint-sakura-room-tryhackme-challanges-easy-2-877b66fe6fbd](https://publication.osintambition.org/osint-sakura-room-tryhackme-challanges-easy-2-877b66fe6fbd)  
8. TryHackMe Sakura Room CTF Write-Up | by Levent Durdalı | Medium, consulté le janvier 4, 2026, [https://medium.com/@leventd/tryhackme-sakura-room-ctf-write-up-47994b800e64](https://medium.com/@leventd/tryhackme-sakura-room-ctf-write-up-47994b800e64)  
9. TryHackMe — Sakura Wakthrough \- Atharva \- Medium, consulté le janvier 4, 2026, [https://atharva39.medium.com/tryhackme-sakura-wakthrough-0b555b7a62b1](https://atharva39.medium.com/tryhackme-sakura-wakthrough-0b555b7a62b1)
