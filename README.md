java c
EECS 388 - Project 5: Forensics 
Fall 2024 
due Thursday, December 5 at 6 p.m.
This project counts for 9% of your course grade. Late submissions will be allowed with the use of late days.
This is a group project; you must work in teams of two and submit one project per team. Note that the final exam will cover project material, so you and your partner should collaborate closely on each part.
Strict no-leaks policy. In this project, you play the role of a computer forensic analyst working to solve a case. Since you don’t want to be fired for jeopardizing an ongoing criminal investigation, you need to follow a strict policy on collaboration. You are bound by the Honor Code not to communicate with anyone regarding any aspect of the case or your investigation (other than within your team or with course staff). The number of pieces of evidence you find, the techniques you try, how successful said techniques are, the general process you follow, etc. are all considered part of your solution and must not be discussed with members of other teams.
Start early. It may be impossible to complete this project before the deadline unless you begin several days beforehand. Please plan accordingly.
Solutions must be submitted via the Autograder and Gradescope, following the submission details at the end of this spec.
To ensure you can get started on-time, please make sure to register your partnership in the Autograder by November 21st @ 11:59 pm
Introduction 
In this project, you will play the role of a forensic analyst and investigate the theft of company secrets from SuperDuperSketchyCorp (SDSC). SDSC became aware of the theft after The Media ran a story regarding one of their closely guarded secrets.
The case went cold when the leading suspect, Leslie Nielson, fled the country and disappeared. Officers seized their computer, but the hard disk was encrypted and investigators were unable to crack the password. No further evidence could be found. The other possible leads are: - Leslie’s Twitter account @LeslieNielson5. - Leslie’s Linkedin.
Investigators just recently caught a break when they found the hard disk encryption password on a sticky note in Leslie’s home office. They’ve decrypted the device and made it available for your analysis.
Your job is to conduct a forensic examination of the disk image and document any evidence related to the crime. If you find sufficient evidence, a case can be brought against Leslie.
Objectives 
Understand how computer use can leave persistent traces and why such evidence is often difficult to remove or conceal.
Gain experience in using forensic techniques to investigate computer misuse and intrusion.
Learn how to retrieve information from a disk image without booting the operating system, and understand why this is necessary to preserve forensic integrity.
Getting Started 
The tools and techniques you use for your investigation are up to you, but here are some suggestions.
General Knowledge 
A working knowledge of Linux is helpful for this project. If you don’t have this yet, you may need to spend time Googling and/or experimenting to get up to speed. The course staff will also answer general Linux questions as a last resort. For an excellent reference book, try UNIX and Linux System Administration Handbook by Nemeth, Snyder, Hein, and Whaley. Also, see https://en.wikipedia.org/wiki/Disk_partitioning for some additional background.
Live Analysis 
Live analysis is a forensic technique in which the investigator examines a running copy of the target system.
HQ has used the disk image of Leslie’s physical computer to produce virtual machine images that might be useful in getting a more holistic view of their activities than can be easily provided by dead analysis (e.g. easily interacting with graphical programs, seeing positioning of files and applications around their computer, etc.). They have provided virtual machine images for VirtualBox and for UTM. HQ heard that you set up a virtual machine in your previous project and thinks that referring back to these skills might be useful here.
From first booting up these images, HQ observed that Leslie may have instituted some measures to prevent their computer from being booted by others, but hopes that you will be able to circumvent these.
Dead Analysis 
In dead analysis, the forensic investigator examines data artifacts from a target system without the system running. We suggest trying dead analysis with the Autopsy open-source forensics tool, which we ship as a Docker image. We have already performed the intensive disk image ingest process using Leslie’s drive, and have provided an Autopsy case which has the analysis available to you to explore.
Running Autopsy in Docker 
1. Download the Autopsy case: leslie-drive.tar.xz.
2. Place this file in the root of your project directory (i.e. on the same level as evidence and tokens.txt ).
3. Decompress the case directory: tar -xJf leslie-drive.tar.xz .
Make sure to decompress the case file in your host, rather than in the development container, as copying files into the development container appears to happen instantaneously but actually takes more time in the background, often causing issues related to decompressing the file while it is still being copied.
4. Open your project directory in VS   Code, then reopen the directory in the development container. See the Docker guide for more information.
5. Once the container has booted, navigate to http://localhost:38805 in your web browser (or vnc://localhost:38855 in a VNC client). After clicking “OK” to the first pop-up, you may be greeted with an empty gray window for some time. It is loading behind the scenes; after a minute or so, you should see the Autopsy home screen pop up.
6. Select “Open Case”, then navigate to /workspaces/project5/leslie-drive and open leslie-drive.aut .
7. After the cas代 写EECS 388 - Project 5: ForensicsR
代做程序编程语言e has been opened, the tree on the left gives you various ways of examining the data. Try expanding “Data Sources” to view the partitions and file system. You can also try running a keyword search using the button in the upper right corner of the window.
8. In addition to hints dropped elsewhere, here is an incomplete list of things to try:
Examine the system logs.
Check for deleted or encrypted files.
Search for strings that may indicate relevance to your investigation.
Password Cracking 
Password crackers may be helpful in trying to brute-force decrypt password-protected files. John the Ripper is the canonical Unix password cracker. Because HQ is confident that John will be useful in your investigation from a cursory investigation of Leslie’s drive, they dedicated time to providing you with it via the project’s development container. HQ, however, does not know what lies ahead and what might be useful as you uncover more; you will be responsible for discovering, obtaining and successfully using tools in other domains throughout the course of your investigation.
When using a password cracker, it is wise to first make sure that the password is not susceptible to a dictionary attack and does not use a restricted character set (e.g., lowercase letters, letters only, letters and numbers only) before spending time on a full brute-force crack. It is also a good idea to crack a very vulnerable password first to make sure you are using the tool correctly.
Like any intensive calculation, password cracking takes time. It may be impossible to dedicate the time required to it if you do not start early enough. Please plan ahead.
Tasks and Deliverables 
The two main deliverables for this project are a list of all the tokens that you find, and a report where you state your case for either the guilt or the innocence of the defendant. In addition, if you recover files that are relevant to your responses, name them in your report and include them with your submission in a tarball named evidence.tar.gz . (Add evidence to the evidence directory then run make to generate this.)
To get you started, here are three questions to ask yourself as you begin your investigation. You do not necessarily have to answer them in the report, but they can serve as good starting points.
1. What operating system does the suspect use?
2. Are there any personal files that the suspect may have left on the machine?
3. Do there appear to be any suspicious usage patterns that suggest malicious activity?
Be on the lookout for evidence of any other machines or network services or websites that the suspect may have used. These may contain important evidence and raise further questions you’ll need to investigate (hint, hint!).
Before attempting to access any such external leads, check with HQ via their self-service portal at SuperDuperSketchyCorp.biz/admin/permissions. If you don’t receive permission, but you still believe a site might be relevant, please email HQ directly at [email   protected]. The subject line should begin with “388 P5 Permission”. Failure to ask permission is guaranteed to be a waste of time and may violate the course ethics policy or result in a grade deduction. You do not need to ask HQ for permission to investigate Leslie’s disk image, Twitter account, or LinkedIn, since you have been cleared to do so by this project spec.
Do not attempt to log in anywhere, besides the permissions site, with your University of Michigan password! We record certain student actions, and we do not want to see your actual password show up in our logs.
The Report 
The report is the focus of your deliverables and will be a substantial portion of your grade. It should specify whether or not Leslie is guilty of a crime. If so, explicitly state the crime and back up this claim with evidence.
Your tokens.txt file serves as a list of your findings. You do not have to specify each of these findings, instead provide a discussion of the most important specific pieces of evidence. Your report should be readable as a standalone document.
The length limit for the report is one page, single spaced. You need to prioritize what evidence you present. Much like a prosecutor would have to in court, you should include pieces of evidence from many distinct sources. While we don’t expect a legal brief, your report should be clear, professional, and easy to read.
The Token List 
The purpose of the token list is to allow us to identify exactly what you found in your investigation. As you complete your investigation, you should be on the lookout for tokens in the form. #token-# or some slight variation of this syntax. All tokens must be spelled exactly as they appear to get credit. Misspelled tokens will receive no credit, with no possibility of a regrade. Including extraneous content in your list will also result in a deduction. The tokens are used for grading only and should not be mentioned in your report.
tokens.txt in your repository should have one token per line, without the surrounding token syntax. Using the same example as above, if you encounter the string #token-# during your investigation, you should only add Thisisthetoken to tokens.txt .
The Evidence Folder 
The purpose of the evidence folder is for you to collect all evidence you deem important to your investigation’s outcome. We may also reference your evidence folder to understand how your investigation progressed. You should not refer to the evidence folder in your report.
There is no strict guideline as to what can belong in the evidence directory; original files or curated screenshots are all acceptable. Filenames and subdirectory structure do not matter.
Run make in the root of your project directory to generate evidence.tar.gz from your evidence directory; you will submit this file to the Autograder.









         
加QQ：99515681  WX：codinghelp  Email: 99515681@qq.com
