# How ***sudo*** **sudoers** ***tar*** can be utilized to have a root access in Linux?
I utilized the machines on https://tryhackme.com/ to do this exercise and it is part of the ***Bounty Hacker*** challenge. The following information helped me solved the challenge:
- ***tar*** on https://gtfobins.github.io/gtfobins/tar/ and https://gtfobins.github.io/
- ***sudoers*** on https://help.ubuntu.com/community/Sudoers
- ***sudo*** on https://www.geeksforgeeks.org/sudo-command-in-linux-with-examples/

1. After obtained access as a regular user to the Linxu machine, I executed the following command:
   $${\color{red}sudo \space \color{lightgreen}-l}$$
   and the result of the command displayed the ***root privilege*** of the regular user account.
   ![](https://github.com/jtoalu/sudo-sudoers-tar-GTFOBins/blob/main/Screenshot%202024-07-06%20234448-redacted.png)
   It means the regular user is allowed to execute ***sudo*** on **tar** which can be used to break out from restricted environments by spawning an interactive system shell.
2. Next step is to execute the following command:
   $${\color{red}sudo \space \color{lightgreen}tar \space \color{lightblue}-cf \space \color{orange}/dev/null \space \color{lightgreen}/dev/null \space \color{lightblue}--checkpoint=1 \space \color{orange}--checkpoint-action=exec=/bin/sh}$$
   Because the ***tar*** binary is allowed to run as superuser by ***sudo***, it does not drop the elevated privileges and we may use it to access the file system, escalate or maintain privileged access.
4. After obtained the ***root*** access, we can execute the following command:
   $${\color{red}cat \space \color{lightgreen}/etc/sudoers}$$
   and we can see the regular user is given ***privilege*** access on **/bin/tar**
   ![](https://github.com/jtoalu/sudo-sudoers-tar-GTFOBins/blob/main/Screenshot%202024-07-09%20185826.png)
   When a regular user is given ***ALL*** privileges (often referred to as “root” or “superuser” privileges) to the tar binary, it means they can perform any action using **tar** without any restrictions. This includes creating, extracting, and modifying archives with full control over file permissions, ownership, and other settings.
5. To remove the ***privilege*** execute the following command:
   $${\color{red}sudo \space \color{lightgreen}visudo}$$
   ![](https://github.com/jtoalu/sudo-sudoers-tar-GTFOBins/blob/main/Screenshot%202024-07-09%20185122.png)

   and remove (comment out) the line to take away the ***privilege***
   
   ![](https://github.com/jtoalu/sudo-sudoers-tar-GTFOBins/blob/main/Screenshot%202024-07-09%20184350.png)
   
Note to Self: https://docs.github.com/en/get-started/writing-on-github/getting-started-with-writing-and-formatting-on-github/basic-writing-and-formatting-syntax and https://stackoverflow.com/questions/11509830/how-to-add-color-to-githubs-readme-md-file
