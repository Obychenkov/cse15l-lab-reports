# Week 1 Lab Report: Tutorial for logging into a course-specific account

## Step 1: Installing VSCode

Start by going to the Visual Studio Code [website](code.visualstudio.com) and follow the instructions to install it for your OS. Once installed, it should look something like this:

![image](https://user-images.githubusercontent.com/122496496/211945088-76f1c83f-0545-47ba-991d-9040b01063f4.png)

## Step 2: Remotely Connecting

Once VSCode is installed, follow the steps in [this](https://stackoverflow.com/a/50527994) tutorial to install and be able to use Git Bash. If done correctly, the top right of the terminal will show "Git Bash" as an option. Click it to create a new terminal.

![image](https://user-images.githubusercontent.com/122496496/211945783-6af0eff5-aa30-404e-9de7-240aa3a689f1.png)

Then, type the following command, with the **???** being replaced with the letters of your course specific account which you can find on [this](https://sdacs.ucsd.edu/~icc/index.php) website after typing in your school username and ID.

`ssh cs15lwi23???@ieng6.ucsd.edu`

After clicking enter, you will likely get a message similar to this:

![image](https://user-images.githubusercontent.com/122496496/211946572-233749c3-c923-46a2-bf0f-adae0236aed1.png)

Type yes and press enter to continue. This message is normal when connecting for the first time, but if you encounter it after connecting to a server often, that might mean someone might be trying to control your connection and you should be cautious.

You will then be prompted to enter a password. If you haven't already, reset your password in the [same location](https://sdacs.ucsd.edu/~icc/index.php) where you found your account details by following the instructions. Be aware that the reset process might take up to 15 minutes, so if entering the password does not work wait some time before trying again.

If successful, your terminal should now look like this, except with your specific account:

![image](https://user-images.githubusercontent.com/122496496/211947123-6c580b04-a1e5-4e23-b0ac-5c264edee48b.png)

You're now connected to a computer in the CSE basement, and any commands will run on that computer.

Some interesting things to note about this step. First of all, every time you connect you will be assigned the ending 201, 202, or 203 after ieng6. This doesn't matter for the rest of the steps in this tutorial, but an example of where this should be noted is if you're running a server, which would change the URL. Another interesting thing you might notice when connecting is that you are given the "cluster status", which lets you know exactly how many people are currently remotely connected to ieng6.

## Step 3: Trying Some Commands

You're now done connecting, here are some (but certainly not all) commands you can try to better understand the difference between your computer and the remote computer: 

* `cd ~`
* `cd ..`
* `pwd`
* `ls`
* `ls -lat`
* `cat /home/linux/ieng6/cs15lwi23/public/hello.txt`

Here's an example of how running some of these commands on the remote computer could look like:

![image](https://user-images.githubusercontent.com/122496496/211948145-538f62a8-47a7-485c-98e6-fb57e10f9592.png)

To log out of the remote server use _Ctrl-D_ or run the `exit` command. 

To conclude with some interesting things you might notice with running the commands: 
1. As you can see in the image above, going back once from the home directory and running ls gives you a list of all the active cse15lwi23 accounts. You can cd into them and run commands like ls, but you will not be able to edit anyone else's files.
2. (Not shown in image) You cannot access any of your local files while on the remote computer. Even though you are still using the same device, no changes, files, folders etc. are shared between the remote and local computers.
