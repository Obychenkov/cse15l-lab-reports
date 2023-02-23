# Week 7 Lab Report: "Done Quick"

The goal of this lab is to use bash to perform a common task of cloning a Git repository, running the tests, fixing the bug, and committing and pushing the fixed version.

## Setup 
### Delete any existing forks of the repository you have on your account
You only need to do this if you have already performed the other steps at least once, and want to try again. Open GitHub and go to the repository. Once there, open the settings tab,
![image](https://user-images.githubusercontent.com/122496496/220791503-0ca92c6c-e8c2-4bad-a408-85cf03d60f8b.png)

Once there, scroll all the way down and delete the repository 
![image](https://user-images.githubusercontent.com/122496496/220791555-70a5e7a3-dc7a-4206-b479-abe65b8cc543.png)

Follow the steps described to delete the fork.

### Fork the repository

Go to the [Lab 7 GitHub Repository](https://github.com/ucsd-cse15l-w23/lab7) and click the "Fork" button on the top right and click the green "Create Fork" button to make a fork of the repository.
![image](https://user-images.githubusercontent.com/122496496/220791876-35f74848-3e93-45d4-9da7-6448e981fb58.png)

## The Competition
Open a new git bash terminal. If you are timing yourself, this is when you'd start the timer. 

### 1. Log into ieng6
Type in `ssh cs15lwi23???@ieng6.ucsd.edu` where the ??? represents your unique string of characters. For example:
![image](https://user-images.githubusercontent.com/122496496/220792545-47260b39-4b4a-40a4-b31c-dbc8dbd9a743.png)

If you have already generated an SSH key for the account, you won't be prompted for a password, which is what my terminal is displaying. If you haven't it will look slightly different as you'll be prompted for a password, but the outcome will be the same.

### 2. Clone your fork of the repository from your Github account

Type in `git clone` followed by the SSH clone link which you can find by clicking the green "Code" button on GitHub
![image](https://user-images.githubusercontent.com/122496496/220792922-8b95e781-beef-4268-9aea-73cf3ea94af0.png)

It look something like this in the terminal: 

![image](https://user-images.githubusercontent.com/122496496/220794018-65387430-e7cd-4d4c-94b8-ced478ae4acd.png)

### 3. Run the tests, demonstrating that they fail

Before running any tests, type in `cd lab7` to enter the directory. It's pretty fast since lab7 is a short name, but if you want to do it slightly faster you can type in `cd l` followed by `<tab>`, which will autofill it to lab7 if you don't have any other directories that start with an l.
Then, type in `javac -cp .:lib/hamcrest-core-1.3.jar:lib/junit-4.13.2.jar *.java` followed by `java -cp .:lib/hamcrest-core-1.3.jar:lib/junit-4.13.2.jar org.junit.runner.JUnitCore TestListExamples` All 3 commands should look like this: 

![image](https://user-images.githubusercontent.com/122496496/220794609-98c447e3-d872-439d-82a1-350d3f5da377.png)

### 4. Edit the code file to fix the failing test

Open the file using a command-line text editor of your choice. I opened it with `vim ListExamples.java`, but `nano ListExamples.java` would also work (small time-saver is to type in `vim Li` followed by a `<tab>` to autofill the rest of the file name. If it autofills to "ListExamples.", type in `j <tab>` to autofill the java part). Here's what the editor looks like with VIM:
![image](https://user-images.githubusercontent.com/122496496/220795129-912da1b5-396e-4e9a-8840-71bba2e837ee.png)

And here's what it looks like with nano:
![image](https://user-images.githubusercontent.com/122496496/220795397-ed44a406-da92-4425-9092-65c9b6a15dd0.png)

The bug occurs on line 43 at `index1 += 1` right before the `return result`, which should be `index2 += 1` for the while loop to not be an infinite loop. I'll split the substeps for this part into VIM and nano.

#### VIM

Once you opened the file with VIM type in the following:

`43 <shift>g e a <backspace> 2 <Esc> :wq`

`43 <shift>g` goes to the beginning of line 43. `e` goes to the end of the next word (at the end of "index1"). `a` enters insert mode after the cursor. Then `<backspace> 2` replaces the 1 with a 2. `<Esc>` exits insert mode back to normal mode, and finally `:wq` writes (saves) the changes and quits VIM.

#### Nano

Once you opened the file with Nano type the following:

`<Ctrl><Shift>- 43,13 <backspace> 2 <Ctrl>X Y <Enter>`

`<Ctrl><Shift>-` (Or `<Ctrl>_`) is a shortcut for going to a certain line and column in the document, where 43 represents the line and 13 represents the column. After that `<backspace> 2` is simply editing the 1 into a 2, then `<Ctrl>X` attempts to exit nano, which will prompt you if you want to save the changes or not, where `Y` represents a yes, and `<Enter>` finalizes the save and exit.

#### More notes

Of course the steps provided aren't the only way to perform the change (and are generally speaking not ideal since they require knowing the line number and the bug). Another way to do it is to use the search feature which both VIM and nano have to search for "index1" in case you don't know the line and column numbers. Or you can always use arrow or movement keys to just get to the end of "index1" in whatever way you want.

### 5. Run the tests, demonstrating that they now succeed

At this point you should have already exited your choice of command-line text editor and are in the terminal. Rerun the tests again to demonstrate the change made in the last step fixed the bug. There are multiple fast ways to do this besides the obvious solution of just retyping the commands in step 3.

#### Arrow keys
Since you have already typed those commands before, it's likely faster to use arrow keys to go back to them instead of typing. Click `<up><up><up><Enter>` to run the compilation `javac` command and then click `<up><up><up><Enter>` again to run the `java` command, the result of which should look like this:

![image](https://user-images.githubusercontent.com/122496496/220799799-5c7b0a44-56dc-4bd4-96b5-53ba6d994bb7.png)

Each time you click the up arrow key, you move up one command you entered previously. So the first time you click `<up>` you should see `vim ListExamples.java` or `nano ListExamples.java` depending on what you used. The next `<up>` you will see the `java -cp .:lib/hamcrest-core-1.3.jar:lib/junit-4.13.2.jar org.junit.runner.JUnitCore TestListExamples` command, and on the final `<up>` you will see `javac -cp .:lib/hamcrest-core-1.3.jar:lib/junit-4.13.2.jar *.java` which is what you want so click enter to run it. The process is similar for the second series of up arrow presses.

The obvious downside of this method is if you didn't run the commands exactly in that order or did other things in-between, you will need a different number of up arrow clicks. It's not an issue as you can see which command you're on as youre cycling through them, so you won't get lost, but if you for example ran `ls` in the middle because you forgot what the file is called, the exact command of `<up><up><up><Enter>` will no longer work for you.

#### Ctrl R Search
This method also relies on the idea that you typed the commands before, but is more consistent than arrow keys for different scenarios. Type in `<Ctrl>r javac <Enter>` to compile. `<Ctrl>r` enters the search mode, "javac" is the string we're searching for which finds the compile command used earlier, and `<Enter>` runs it.

The small complication occurs in the next step because to run the tester you need to use `<Ctrl>r java <Ctrl>r <Ctrl>r <Ctrl>r <Enter>`. By default, the search will find the latest command that has the given string, which in this case is the command we just ran with "javac", pressing `<Ctrl>r` twice will cycle it to the command before that which is `vim ListExamples.java`, and the last `<Ctrl>r` will show the correct `java -cp .:lib/hamcrest-core-1.3.jar:lib/junit-4.13.2.jar org.junit.runner.JUnitCore TestListExamples` command.

In this case, what method you use doesn't matter as much as the tests were ran right before editing the file. But if you ran them initially and then had to open editors for multiple files while going in and out of multiple directories and performing other tasks in between, the `<Ctrl>r` method is probably a better bet.

### 6. Commit and push the resulting change to your Github account

Finally, we need to commit and push our changes to the repository. First, run `git add ListExamples.java` (again using tab after typing `git add Li` if you wish) before the next step. To commit, type in `git commit -m "(YOUR MESSAGE GOES HERE)"` with any message you want. The message won't change any functionality, but it's a good practice to make the messages short but descriptive of the changes you made. Finally, type in `git push origin` to push the changes. The whole process looks like this:
![image](https://user-images.githubusercontent.com/122496496/220801927-89eb1c9e-711c-4410-80e7-04277423a7a4.png)

You're now done and can pause your timer. Go through the process multiple times, trying the different options listed and see if you can do it faster!
