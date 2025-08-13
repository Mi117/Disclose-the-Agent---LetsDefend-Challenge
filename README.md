# Disclose-the-Agent---LetsDefend-Challenge
Unmasking the Operative: A Step-by-Step Forensic Analysis of SMTP Traffic and Hidden Clues

![agentsmith](https://github.com/user-attachments/assets/6a65ca36-d278-4893-bb51-767f159f56fa)


### SCENARIO

We reached the data of an agent leaking information. You have to disclose the agent.

Log file: /root/Desktop/ChallengeFile/smtpchallenge.pcap

Note: pcap file found public resources.

Link to the Challenge: [https://app.letsdefend.io/challenge/disclose-the-agent]

---

### TOOLS USED

- Cyberchef [https://gchq.github.io/CyberChef/]
- Wireshark [https://www.wireshark.org/]
- Linux Terminal

---

### WALKTHROUGH

We start our investigation by opening the .pcap file and inspect the packet traffic using **Wireshark**. We then proceed on answering our questions.

### 1) What is the email address of Ann’s secret boyfriend?

Bearing in mind the key term ‘email address’, we proceed to analyze packets that involve the **STMP protocol — the Simple Mail Transfer Protocol**, used for sending and receiving email over the Internet.

<img width="1892" height="799" alt="1  smtp discovery" src="https://github.com/user-attachments/assets/22658d65-f847-4ce3-a960-346d70fb9ea5" />

From the screenshot we can see already valuable information about the User such as their credentials for the login process and also the email sent to their target destination:

- the parameter ‘**AUTH LOGIN**’, requested for User authentication;
- ‘**EHLO annlaptop**’ : possibly the machine name from where the request for User auth came originated;
- **USER:** **c25lYWt5ZzMza0Bhb2wuY29t** (Base64 Cryptographed username);
- **PASS: NTU4cjAwbHo=** (Base64 Cryptographed password);

<img width="1596" height="279" alt="1 3 credentials" src="https://github.com/user-attachments/assets/46ce8628-9a39-418a-9aec-776821032bf4" />

We then go on by analyzing the data traffic to find the information we need about Ann’s boyfriend email. By following the TCP Stream of such data, we can clearly identify another email address, quite certainly the secret boyfriend’s.

<img width="1750" height="592" alt="1 4 analyze packets email" src="https://github.com/user-attachments/assets/cd7ba7a9-f2f8-44fd-b430-6bcec178db72" />

<img width="1280" height="829" alt="1 5 email reveal" src="https://github.com/user-attachments/assets/ceceb439-f451-4461-8a22-cff6f0fd2d12" />

The suspicions are also corroborated by the stark loving message contained in the email.

<img width="1268" height="818" alt="1 6 message loe" src="https://github.com/user-attachments/assets/3c21b08b-afb9-4c79-8ec7-31a59377c99e" />

### 2) What is Ann’s email password?

To answer this question we use the **CyberChef** tool — decoding the previously identified password from **Base64.**

<img width="1612" height="829" alt="2  password decode" src="https://github.com/user-attachments/assets/27697d9f-77da-45ba-a4be-f690afff929d" />

### 3) What is the name of the file that Ann sent to his secret lover?

By analyzing the data packets, we can find the code of a file attached to the email, clearly out target file.
The name is displayed in the `Content-Disposition: attachment; Filename=”secretrandexvous.docx”` section of the **TCP Stream analysis**.

<img width="1279" height="828" alt="3  secret message" src="https://github.com/user-attachments/assets/23a2d84d-3e6c-42f8-92ac-ccc6e3cf06e9" />

### 4) In what country will Ann meet with her secret lover?

To answer the question we need to analyze the previously discovered file. On **Wireshark** we head to `File > Export Objects > IMF`.

<img width="1137" height="833" alt="4 1 get the file" src="https://github.com/user-attachments/assets/a353c652-178b-47b9-9725-762365545cfa" />

<img width="928" height="703" alt="4 2 file downloaded" src="https://github.com/user-attachments/assets/43c30933-1d84-43a5-9ca8-63a6a8c5eda1" />

This option allows us to download the IMF — Internet Message Format file on our machine as an `.eml` file, that we can then open with our email client or text editor of choosing.

<img width="1268" height="829" alt="4 3 opent the atatched file" src="https://github.com/user-attachments/assets/c6d7466f-5111-4315-8c0e-9be5aa694737" />

<img width="672" height="504" alt="4 4 open the file" src="https://github.com/user-attachments/assets/a26cf47f-1d46-4242-83fd-327715806e71" />

Once opened the secret meeting location is easily revealed:

<img width="1913" height="852" alt="4 5 file content" src="https://github.com/user-attachments/assets/5eec7257-a0df-4ed2-9e7b-c4d8a5674fc5" />

### 5) What is the MD5 value of the attachment Ann sent?

We open a Terminal window in our directory, and get the md5 file hash with the related command.

<img width="1024" height="711" alt="6  file hash" src="https://github.com/user-attachments/assets/d8de1c09-c86d-4e0b-b0ed-0d3604c8cc24" />

--- 

## Conclusion and Final Thoughts 

Concluding this Disclose The Agent walkthrough, I’m struck by how elegantly this challenge integrates foundational DFIR skills within a compact, yet thought-provoking scenario. From the initial SMTP packet filtering in Wireshark to the final MD5 hash extraction of the recovered attachment, each step reaffirmed the power of methodical analysis underpinned by essential tools and techniques.

**Key Takeaways**:
- **SMTP analysis revealed human insights**. Filtering the PCAP for SMTP and following TCP streams was instrumental in uncovering the secret lover’s email address, the base64-encoded credentials, and the attached document — all fundamental to piecing together the narrative.

- **Decoding and reconstruction are indispensable**. Whether using CyberChef or command-line utilities, decoding base64 strings and reconstructing the .docx file vividly demonstrated how seemingly mundane data can contain highly sensitive information.

- **Metadata matters**. Extracting and verifying the MD5 hash of the attachment reinforced the importance of cryptographic validation — especially when handling recovered artifacts in digital investigations.

In essence, the Disclose The Agent lab reaffirmed that behind every packet lies a story, waiting to be unearthed with the right combination of focus, tools, and curiosity. I’m grateful for the opportunity to refine these skills through such a well-structured yet realistic scenario, and I look forward to tackling the next challenge with the same analytical rigor and enthusiasm.

---

I hope you have found this Write-Up insightful and make sure to follow me on all the platform to stay up-to-date with my latest analysis, write-ups and be part of my journey into the world of Cybersecurity!
Link: [https://linktr.ee/atlas.protect]










