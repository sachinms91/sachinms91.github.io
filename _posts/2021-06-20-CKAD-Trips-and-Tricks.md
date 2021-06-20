---
title: Trips and Tricks for CKAD exam
author: Sachin M S
header-img: "https://cdn.jsdelivr.net/gh/sachinms91/blog-images/images/thumbnails/ckad.png"
date: 2021-06-21 00:30:00 +0800
categories: [Technology, Kubernetes]
tags: [CKAD]
image: "https://cdn.jsdelivr.net/gh/sachinms91/blog-images/images/thumbnails/ckad.png"
---

### Tips and tricks to ace CKAD exam!

![Badge](https://cdn.jsdelivr.net/gh/sachinms91/blog-images/images/thumbnails/ckad.png)

 I had appeared for Certified Kubernetes Application Developer (CKAD) exam and cleared it successfully. The Certified Kubernetes Application Developer exam certifies that users can design, build, configure, and expose cloud native applications for Kubernetes.
A Certified Kubernetes Application Developer can define application resources and use core primitives to build, monitor, and troubleshoot scalable applications and tools in Kubernetes.It is an open-book exam. 

The online, proctored, performance-based test consists of a set of performance-based items (problems) to be solved in a command line and is expected to take approximately two (2) hours to complete.

This exam curriculum includes these general domains and their weights on the exam:

1. 13% – Core Concepts
2. 18% – Configuration
3. 10% – Multi-Container Pods
4. 18% – Observability
5. 20% – Pod Design
6. 13% – Services & Networking
7. 8% – State Persistence

I would not delve into tips of exam which are pretty much out there in tons of the other articles. I would like to highlight points whatever I felt were missing out according to me.

Below are my two cents advice which might be helpful:
1. First and foremost, if you are not familiar or don’t have exposure to Linux operating system/Linux terminal commands then I would recommend taking a crash course on Linux.I would suggest this  [LinkedIn learning course](https://www.linkedin.com/learning/learning-linux-command-line-2/learning-linux-command-line?u=68385001) {:target="_blank"}. Knowledge of the Linux command line is critical for anyone who uses this open-source operating system. For many tasks…

2. Imminently, practice is the key for the exam. Try to skip questions with low weightage by flagging them and attend them towards end if time permits. Time management is the key for the exam.
3. Go through all “Tasks” section of official Kubernetes documentation page. If possible, bookmark all tasks accordingly as they would be handy for quick search.
4. A set of exercises that helped me prepare for the Certified Kubernetes Application Developer. Practice below questions from below GitHub repository:
 [dgkanatsios/CKAD-exercises](https://github.com/dgkanatsios/CKAD-exercises){:target="_blank"}
5. Few of Linux flags which I had made notes
 -  Example: 
``` grep -i ‘annotations’ ```
-i -> case insensitivity
 -  ```echo -e ‘var1=val1\n var2=val2’```
The ‘-e‘ option in Linux acts as interpretation of escaped characters that are backslashed.
 - ```echo -n```
-n option can be used to remove the ‘\n’ (newline character) from the output. By default, echo includes ‘\n’ at the end of every string it outputs
6. If you practice with Vim editor below trips would be helpful.
- $ goes to the end of line, remains in command mode
- ‘A’ goes to the end of line, switches to insert mode
- ‘dd’ cuts a line
- To jump to particular line — In command mode type line number followed by ‘G’
- ‘dG’ — Deletes contents from cursor to end of file. This is very useful when editing YAML files.
- ‘ZZ’ — Save and exit quickly.
- ‘3yy’ — Yank (copy) three lines, starting from the line where the cursor is positioned.
7. Concentrate on difference between CMD and ENTRYPOINT difference in docker. Again I would recommend Zeal Vora’s course for this.
8. Remember to memorize the options for “kubectl run” rather than using “explain” command

```kubectl run NAME — image=image [ — env=”key=value”] [ — port=port] [ — dry-run=server|client]```
```[ — overrides=inline-json] [ — command] — [COMMAND] [args…] [options]```

9. Use kubectl ‘Explain’ command with recursive flag and ‘less’ as shown. This would help to show output without overwhelming text throughout the terminal.

```kubectl explain cronjob.spec.jobTemplate — recursive | less```
10. Persistent Volume (PV), Persistent Volume Claim(PVC) and NetworkPolicy objects cannot be created using imperative commands hence remember write yaml from scratch.
11. Concentrate on logging feature of k8’s. Logging pattern with Adaptor/Side car container pattern would be helpful. I would recommend Zeal Vora’s CKAD course on Udemy for this topics as he has covered all topics on logging pretty well.
12. VIM settings edit with “vi ~/.vimrc”

```set nu```
```autocmd FileType yaml setlocal et ts=2 ai sw=2 nu sts=0```
```set paste```

13. Use “Ctrl+d” to exit a container when you are running bash shell on a container inside a pod or type ‘exit’
14. To indent multiple lines using vim you should set the shiftwidth using :set shiftwidth=2. Then mark multiple lines using Shift v and the up/down keys.To then indent the marked lines to Shift . or Shift ,
15. Practice exams from [killer.sh](https://killer.sh/){:target="_blank"}. Questions from here are more tougher than the ones which appear in exam. Please dont assume that this is some sort of question dumps for exam.

Wishing you the best of luck if you are planning to take up the exam! Feel free to connect with me for any queries :)


