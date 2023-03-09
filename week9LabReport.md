# Week 9 Lab Report: Lab Report 4 Using a Bash Script

## Intro
This report is referencing Lab Report 4 titled ['Week 7 Lab Report: "Done Quick"'](https://obychenkov.github.io/cse15l-lab-reports/week7LabReport.html). The goal of it was to perform a series of tasks such as cloning a Git repository, running the tests, fixing the bug, and committing and pushing the fixed version. The focus in every step was to use command line techniques, options, and shortcuts to get this done as fast as possible. 

However, the premise of it was that you weren't allowed to use a bash script. In this lab report, I'll be detailing how all of the steps can be simplified into one bash script which will allow you to perform all of those operations significantly faster.

## Step 1: Log into ieng6 
Unfortunately, this is a step you have to do before making a bash script. Why? Because the login command itself is not considered finished until you exit the remote connection, so none of the following commands in the bash script won't run until you exit them, here's an example of what I mean:

Given the following code in a bash script:
```
ssh cs15lwi23acs@ieng6.ucsd.edu

echo "Hello"
ls
```
The output will be:

![image](https://user-images.githubusercontent.com/122496496/223882250-97517090-b4ad-4b1b-a9d3-ca4d6e8dba6f.png)

As you can see, `echo "Hello"` and `ls` are executed only after I've exited, which is obviously not the intention as all the commands should be ran on the remote computer. 

Therefore, type in `ssh cs15lwi23???@ieng6.ucsd.edu` where the ??? represents your unique string of characters. See the original lab report for more details.

## Setting up a bash script

You should already be logged in so use the command line to make a new bash file which ends with `.sh` using your command line editor of choice. I'll use `vim doneQuick.sh` but other editors like `nano doneQuick.sh` work too. I won't be going into detail on how to navigate the editor as that will differ for everyone and isn't the main goal of this lab.

### Step 2: Clone your fork of the repository from your Github account

Type in `git clone` followed by the SSH clone link which you can find by clicking the green "Code" button on GitHub inside of your bash file.
![image](https://user-images.githubusercontent.com/122496496/220792922-8b95e781-beef-4268-9aea-73cf3ea94af0.png)

### 3. Run the tests, demonstrating that they fail

Before running, make sure to add the line `cd lab7` to change the working directory to the cloned one. Then add the lines `javac -cp .:lib/hamcrest-core-1.3.jar:lib/junit-4.13.2.jar *.java` followed by `java -cp .:lib/hamcrest-core-1.3.jar:lib/junit-4.13.2.jar org.junit.runner.JUnitCore TestListExamples` to compile and run the tester.

### 4. Edit the code file to fix the failing test

Here's where using bash allows a slight deviation that is not always practical but for this specific purpose works quite well. At this stage we'd normally open the file ListExamples.java using a command line editor and fix the issue. However, this can actually be done in just 1 bash line since we know the exact location where the issue occurs. 

Add the following to the bash script: `sed -i '43s/index1/index2/' ListExamples.java`

The `sed` command is used for a variety of text editing options, but with the `s` option is used to substitute text. In this case, we are saying that on line 43 we want to replace "index1" with "index2" and the `-i` option allows the command to make that change on the file in place.

The obvious downside of this is that we obviously need to know exactly what the issue is and the exact line it's on, so it's not practical for a wide variety of cases, but it works well in this scenario.

### 5. Run the tests, demonstrating that they now succeed
Simply add the lines `javac -cp .:lib/hamcrest-core-1.3.jar:lib/junit-4.13.2.jar *.java` followed by `java -cp .:lib/hamcrest-core-1.3.jar:lib/junit-4.13.2.jar org.junit.runner.JUnitCore TestListExamples` to the bash script again to recompile and run the tests again.

### 6. Commit and push the resulting change to your Github account

Add the lines `git add ListExamples.java`, `git commit -m "(YOUR MESSAGE GOES HERE)"` and `git push origin`. And you should be done!

## Final Bash File, Output, and Improvements

Here's what the final Bash file should look like (with names and messages replaced as appropriate)
![image](https://user-images.githubusercontent.com/122496496/224172343-7d09f12e-3f4f-452a-88aa-81c5e1391be3.png)

And here's what the output of running `bash doneQuick.sh` looks like (note: it's not split, the output just didn't fit in one screenshot):
![image](https://user-images.githubusercontent.com/122496496/224172990-b26a228d-2b27-46f7-b938-15502eaf823a.png)
![image](https://user-images.githubusercontent.com/122496496/224173028-e67ac190-8379-416e-8e8c-49db78125f5e.png)

Now whenever we want to perform all of these operations all we have to do is manually connect to the remote computer and just run the bash script which takes less than 10 seconds total. 
If you wanted to do this with another repository you'd change the clone, the `cd`, the replacement in the `sed` command, and the file names for the testers and the `git add` command which is once again faster than doing all of this by hand, so this bash script can still be useful for other scenarios.

However, one minor issue is that the output is a bit messy and hard to interpret. This isn't an issue in this case as we know those steps do what we need to, but if you made any mistakes or want to show this to someone else, they might be confused by the wall of text, so let's add some cleanup to the bash script.

Here's the new bash file contents:
![image](https://user-images.githubusercontent.com/122496496/224175426-e3353d76-6fad-4838-96ea-d227d80d99f1.png)

And here's the neater output: 

![image](https://user-images.githubusercontent.com/122496496/224175306-42ebcc80-39db-45f1-a9f0-b643141d19ad.png)
![image](https://user-images.githubusercontent.com/122496496/224175334-0156c140-555c-4228-85d3-8e304b0f1eb5.png)

Obviously not the most elegant solution, but it still helps us figure out what stages we are at and creates some space in between steps for better readability.

Another option bash provides is checking for exit codes which I won't add but still worth mentioning. If we didn't know whether TestListExamples.java existed for example, we'd write code like this
```
if [[ -f TestListExamples ]]
then 
    echo "TestListExamples found"
else
    echo "Exit code:" $?
    echo "File TestListExamples.java not found, check if file is named correctly"
    exit
fi
```

This code checks if a file named TestListExamples exists and if it does outputs a confirmation message but otherwise reports the exit code and the issue and exits the bash script without running any further code. This is good because if TestListExamples.java didn't exist due to being put in the wrong directory or a typo, then that part of the bash script would fail, but it would attempt to run the testers anyways which would just make a mess that might be hard to untangle when reading that output from the terminal. So do consider adding in simple if statements to ensure the bash script does exactly what you want it to do and exits smoothly and makes the error clear whenever things go wrong. 


