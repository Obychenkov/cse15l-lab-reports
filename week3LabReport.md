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

## Part 2: Inputs, Symptoms, and Bugs

Here's a code sample that's intended to reverse an array by returning a new array with all the elements of the original in the reversed order without altering the original array:

```
static int[] reversed(int[] arr) {
    int[] newArray = new int[arr.length];
    
    for(int i = 0; i < arr.length; i += 1) {
      arr[i] = newArray[arr.length - i - 1];
    }

    return arr;
  }
```

However, it includes a bug that makes it not function as intended. Let's check what's wrong with a simple JUnit test:

```
  @Test
  public void testReversed() {
    int[] input1 = {1, 2, 3, 4, 5};
    assertArrayEquals(new int[]{5, 4, 3, 2, 1}, ArrayExamples.reversed(input1));
  }
```

Given a simple array `{1, 2, 3, 4, 5}`, the intended output is `{5, 4, 3, 2, 1}`. 

Here's another JUnit test for the same method that is a bit silly but will help demonstrate a point later on: 

```
  @Test
  public void testReversed() {
    int[] input1 = {0, 0, 0};
    assertArrayEquals(new int[]{0, 0, 0}, ArrayExamples.reversed(input1));
  }
```

Let's see what happens when the two tests are run: 

![image](https://user-images.githubusercontent.com/122496496/214997277-0b9737d9-7bed-4854-a955-a4987f588042.png)

Important to note that the second test did not return an error. So the symptom we see is that the first element of the new array is 0 instead of 5, which is interesting since the original array doesn't even include a 0 in the first JUnit test. Go back to the code segment at the start of the section and see if you can discover what the bug was.

Here's the code segment fixed:

```
static int[] reversed(int[] arr) {
    int[] newArray = new int[arr.length];
    
    for(int i = 0; i < arr.length; i += 1) {
      newArray[i] = arr[arr.length - i - 1];
    }

    return newArray;
  }
```

The simple fix is swapping `newArray` and `arr` inside the for loop and returning `newArray` instead of `arr`. The issue was that `newArray` was created, but never filled with any values (therefore being an array filled with zeroes). In the for loop, `arr` was copying the values (zeroes) from `newArray`instead of vice versa, and `arr` was then being returned instead of `newArray`. This means regardless of the input, the output would be an array with the same number of elements but all replaced with zeroes. The fix ensures that `newArray` copies the values from `arr` in reversed order in the loop, and is then returned.

Back to the second JUnit test, in this case it should be obvious it's not a great test. Yet, it helps show that sometimes you can find a piece of hay in a needlestack. It passed even while the method had a bug, just demonstrating that even if a test passes, it shouldn't immediately be concluded that all the code functions as intended.

## Part 3: What did I learn?

From part 1 (Lab 2), I learned a way to use the URL to change the page. It's sometimes funny to click a link on a website and see the URL fill the entire width of the bar with a bunch of digits and special characters. That's not a mistake, that's just a way of implementing certain features.

From part 2 (Lab 3), I learned the importance of JUnit tests. Let's be honest, most of us love just adding print statements in the middle of the code and figuring it out that way. However, JUnit tests are easier to implement, faster to run multiple of, and help pinpoint the bug easier. For shorter programs or programs you wrote yourself and know very well, the print strategy might work. Yet, for longer programs or code you didn't write yourself, it's easier to run tests and then figure out where the problem might be instead of going through and understanding all the code.
