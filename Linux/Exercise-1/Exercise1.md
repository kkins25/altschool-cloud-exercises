# Exercise-1
While the instructions provided by the instructor were crispy clear, I encountered two major issues- the first due to my own impatience, and the second probably due to case scenario_2(see below).<br>

## Problem 1: Slow download of vagrant box in command line/git bash
<br>

At first, I didn't think the box(unbuntuu/focal64) was being downloaded. Since i wasn't getting realtime update. So I researched to find out where the box was being downloaded to. I discovered that the downloading box was stored in a hidden file ***vagrant.d/tmp***. Ater a while i realised that the box was downloading albeit very slowly. So, I closed the terminal and went straight to the vagrant website to download the box. It was super faster! 

### Then came the next problem...
<br>

Running <code>vagrant init ubuntu/focal64</code> was still trying to download the box :(.

### So, what did i do to solve this? 
Another round of running through different websites till i found the right one [here](https://stackoverflow.com/questions/22065698/how-to-add-a-downloaded-box-file-to-vagrant)
<br>
<code>
>vagrant box add my-box name-of-the-box.box
>
>vagrant init my-box
>
>vagrant up
</code>

finally! Vagrant created the container for my local ***ubuntu/focal64***. pheww! :)

<br>
Everything seemed to run smoothly until i came across a comment: 
<br>

![Bad Belle Comment](/altschool-cloud-exercises/Linux/Exercise-1/badbelle.jpeg "Life saver")


<br>

### My <code>ifconfig</code> output only had two "outputs".
<br>

![First Trial](/altschool-cloud-exercises/Linux/Exercise-1/firsttrial.jpeg "No dhcp")
<br>

My world turned upside down, I was being swallowed into the belle of a turbulent ocean. Then my perils continued for the next 2 hours. Having worked on this exercise over night, i figured "meh, my brain is probably fried." So I took a long nap. 4 hours later, I tried again and discovered the problem. 

## Problem 2: Ifconfig not launching "dhcp"
From my research, the error arose due to either of the two main reasons: 

* **Case Scenario 1:** Conflicting error due to Virtual box being run in by another vitual machine?

* **Case Scenario 2:** Vagrant bug claimed to exist in some ***vagrant versions***? 

<br>

## Solution: 
I copied a vagrantfile configuration to fix the bug [from here](https://github.com/hashicorp/vagrant/issues/8878#issuecomment-345112810). I inserted the code into my vagrantfile via Gitbash with command <code>nano vagrantfile</code>
<br>

><code>
>class VagrantPlugins::ProviderVirtualBox::Action::Network
>
>&nbsp;&nbsp;def dhcp_server_matches_config?(dhcp_server, config)
>
> &nbsp;&nbsp;true
>
> &nbsp;end
>
>end
></code>

<br>

### Finally; 
It is running fine now. I guess:>

![Ifoconfig screenshot](/altschool-cloud-exercises/Linux/Exercise-1/ifconfig.jpeg "ifconfig screenshot")