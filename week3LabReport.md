# Week 3 Lab Report: Servers and Bugs

## Part 1: StringServer

![image](https://user-images.githubusercontent.com/122496496/214931805-095486d4-6798-465b-8032-af1244e9dca5.png)

**Image 1: Code for the StringServer class**

![image](https://user-images.githubusercontent.com/122496496/214932158-d9807be4-7dd0-4fd6-bd7d-5dbb11b53ad5.png)

**Image 2: Page after using add-message?s=Apple in the URL**

![image](https://user-images.githubusercontent.com/122496496/214932325-6fe00974-d9f3-457f-a134-7fc929edcb77.png)

**Image 3: Page after using add-message?s=Banana in the URL following image 2**

This is a simple web server `StringServer` that stores a single string which can be added to by changing the path in the URL. 

In images 2 the first method ran is the `main` method from the `StringServer` class which is responsible for starting a new server on the given port, and initializes a new `Handler` object from the same class (shown in the top half of image 1).

Then, the `handleRequest` method from the `Handler` class is being called. The only argument of the method is `url`, which is a `URI` class object that allows to access, manipulate, and extract information from the URL. The relevant instance variable is the `output` string that starts empty but gets filled up as words get added. 

The method breaks down the path in the URL (which is automatically given as a parameter whenever the page is loaded) to check if it contains the string "/add-message". If it does, then if the path is formatted in the following way: *add-message?s=* followed by any string, the string after the equals sign will be appended to the `output` string (along with `\n` which is the newline character) and printed on the screen. This is done by breaking up the part before the equals sign and the part after into two separate items in the `parameters` String array and using the second element for the output. In this specific case, the string "Apple" is added to output and printed on the screen.

In image 3, you can see the same `handleRequest` method being called same as in image 2. The only difference is that the `output` variable already contains the string "Apple \n" instead of being empty. Since the main method wasn't ran again since the server is already running on the same port, a new `Handler` object isn't created, so `output` is maintained. However since the page was reloaded due to the URL changing, the `handleRequest` method is ran. It follows the same rules as described before, but this time adds the string "Banana \n" to `output`. Therefore now `output` equals "Apple \n Banana \n", which results in Apple and Banana being printed on the screen on separate lines.

## Part 2: Inputs, Symptoms, and Bugs**

## Part 3: What did I learn?
