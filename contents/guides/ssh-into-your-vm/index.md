---
title: SSH Into Your VM
author: leeolayvar
template: guide.jade
---


In this tutorial, we will go over the steps to SSHing into your VM! This
is a semi-experimental tutorial, so if you have any problems please make
sure to
[submit an issue](https://github.com/leeolayvar/koding-unofficial/issues/new)
and we can help make this a rock solid tutorial for all skill levels :)

Note that we will only be covering Unix based OSs. If someone wants to
give me information on how this can be done on Windows, i'll be happy
to add a windows section!

**Reminder**: As with all of these tutorials, they assume that there are no
conflicts. If you have previously attempted to install this software please
remove it fully or understand that conflicts may occur. Thanks :)



## Video

The following is an instructional video which approximately
mirrors the steps below. It covers both App, and Manual,
installations.

<iframe width="680" height="450" src="//www.youtube.com/embed/h_l6hElWoj4" frameborder="0" allowfullscreen></iframe>



## What you will need

In this tutorial, i am going to use the terminology of "Home" and "Koding"
machines. Home being whatever the machine you are using to connect to
Koding with. Koding being the machine that is receiving the connection.
Home -> Koding.

On the home machine, you will need a public rsa key *(usually found
in `~/.ssh/id_rsa.pub`)*. If you need to generate one, please
[refer to the Github tutorial on this](https://help.github.com/articles/generating-ssh-keys).
You will also need your Username, and your VM Number.

To find your VM number, open your terminal for the VM you wish to ssh into,
and look for the *username@vm-0:~$*, where *vm-0*, *vm-1*,
*vm-2*, etc, is your vm number.

**Feedback**: If you feel Generating an SSH Key would be very helpful on this
tutorial, feel free to
[let me know](https://github.com/leeolayvar/koding-unofficial/issues/new) :)




## Tutorial Steps

1. First, copy your Public Key, usually found in `~/.ssh/id_rsa.pub`, and copy
  it in it's entirety! It will look something like this:
  
  ```
  ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAABAQCyhKankDE4DRM86JqZ3JPdWDeqg+TbzlqlTLf
  OKTeokhRoMgy5WoMY/ZWUVES3d2vSHHwW3cwWlELmVdc3Ow57boZv3fOsPhybYHVRTClXYr1ncS
  xyTvjvCfvV5q22aIxHPWQ353543ssda87sa+85XEa4VnveJsEzxBZl4oJ4GB0AGa48+UdIqutrg
  Zu7D7JCK+Yl228X+3bJf3ddlqDaKaVXPivvvYqImK6ZwFsxh2lNO4E8IOd3OSK9zv6i+io8PxWm
  wP0tLFokxulAI8Td1sOPBE9s9bdJ5c2T/GfGjKF+aNKsd33TsYEjjc/plMZmRRrOgQwre6OAkgM
  vyV2X foo@bar.baz
  ```
  
2. Next, paste this entire Public Key into your SSH Keys section of your
  Account settings. This can be found by going to
  [koding/Account](https://koding.com/Account) and clicking SSH Keys
  under the DEVELOP. Click the Plus button on the right side of the page,
  and paste your Public Key into this. Below is a screenshot of this area
  for clarification.
  ![Koding SSH Keys](sshkeys.png)
  
3. Now go back to your Home machine, and create the file
  `~/.ssh/config` *(assuming it's not already created)*. Add the following
  code into that file:
  
  ```
  Host *.kd.io
    User <username>
    ProxyCommand ssh %r@ssh.koding.com nc %h %p
  ```
  
  Where `<username>` is your username, without the `<>`.
  
4. Next, on your Home machine and connect to your VM! This can be
  done by typing: `ssh <vm-Number>.<username>.koding.kd.io`. An example,
  here is my connection command: `ssh vm-0.leeolayvar.koding.kd.io`.
  
  You will have to enter your local SSH password, if you chose one when you
  created your key. After that, presented with `username@vm-X:~$`, singaling
  that you have connected successfully.
  
  #### Possible Gotcha: ~/.ssh/authorized_keys
  
  You do *not* need to use authorized_keys in the Koding VMs. The
  Account Settings -> SSH Keys takes care of the authorization for you.
  
  #### Possible Gotcha: Agent admitted failure?
  
  If you receive an error when you attempt to connect, matching the following
  description:
  
  ```
  Agent admitted failure to sign using the key.
  ```
  
  Then run the command `ssh-add`. For additional information on this gotcha,
  see the
  [Github Help Page](https://help.github.com/articles/error-agent-admitted-failure-to-sign)
  on the subject.



## Confirming your Installation

The best way to confirm your installation is simply by connecting to your
Koding VM. For information on this, see Step #3 above.



## Additional Resources

- [Agent Failure Information](https://help.github.com/articles/error-agent-admitted-failure-to-sign)

