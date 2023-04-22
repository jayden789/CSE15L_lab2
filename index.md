# Lab 2 Report: Servers and Bugs
## Part 1
Code for **StringServer** and **/add-message**
```
import java.io.IOException;
import java.net.URI;

class Handler implements URLHandler {
    // The one bit of state on the server: a number that will be manipulated by
    // various requests.
    String str = "";

    public String handleRequest(URI url) {
        if (url.getPath().equals("/")) {
            return str;
        } else {
            System.out.println("Path: " + url.getPath());
            if (url.getPath().contains("/add-message")) {
                String[] parameters = url.getQuery().split("=");
                if (parameters[0].equals("s")) {
                    str += parameters[1] + "\n";
                    return str;
                }
            }
            return "404 Not Found!";
        }
    }
}

class StringServer {
    public static void main(String[] args) throws IOException {
        if(args.length == 0){
            System.out.println("Missing port number! Try any number between 1024 to 49151");
            return;
        }

        int port = Integer.parseInt(args[0]);

        Server.start(port, new Handler());
    }
}
```
**First example**
`add-message?s=Friday`

![friday](https://user-images.githubusercontent.com/112384009/233758057-733e3692-f1b4-4620-98d3-1b7ca8797aed.jpg)

---
* The method called is `String handleRequest(URI url)`, it returns a String object, which is what we want to display on webpage.
Also there are some other methods being called like `getPath()`, `contains()`, `equals()`, `getQuery()` as helper methods 
in processing the url.

* The `Server.start(port, new Handler())` then uses the port we provided on the command line (**4000**), a Handler object to start
a server and process the url we give.


* There are two classes `Handler` and `StringServer`, the `Handler` class has `str` field, which gets updated everyt time
we change the **s query**.
* The `String handleRequest(URI url)` needs an url **http://localhost:4000/add-message?s=Friday**
object to process our request, look for the path to check for certain things.
* If the path contains `/add-message` (*which it does in this example*), then it will check the query (which starts after **?**)
it splits the string querty into list of strings separated by **=** sign, and update the content after the **=** sign and prints
out on the webpage.

* In this example, we the intial string `str` is an empty string, and we give query ( after the `**?**`) `s=Friday`.
* The url we give after being processed by `handleRequest(URI url)` method will update the str (which is **Friday**) now and prints out on the webpage.
 

![sat](https://user-images.githubusercontent.com/112384009/233760030-c07bdd22-f21b-45dc-a899-8c2279d77307.jpg)

**Second example**
`add-message?s=Saturday`

* The method called is `String handleRequest(URI url)`
 and some other methods being called like `getPath()`, `contains()`, `equals()`, `getQuery()` as helper methods 
in processing the url.

* The `Server.start(port, new Handler())` then uses the port we provided on the command line (**4000**), a Handler object to start
a server and process the url we give.

What are the relevant arguments to those methods, and the values of any relevant fields of the class?
* For the second example, the url is ***http://localhost:4000/add-message?s=Saturday***, as we change the value of query s to `s=Saturday`
* The `str` field of `Handler` class get updated to **Friday** (with newline being concatenated at the end) after we give the first url.

How do the values of any relevant fields of the class change from this specific request? If no values got changed, explain why.
The `str` field after url being requested gets updated to
``` 
Friday
Saturday
```
(with newline being added at the end).

## Part 2
Here is the code that has bug:
```
  // Changes the input array to be in reversed order
  static void reverseInPlace(int[] arr) {
      for (int i = 0; i < arr.length; i += 1) {
        arr[i] = arr[arr.length - i - 1];
      }
  }
  ```
**A failure-inducing input**
```
public class ArrayTests {
	@Test 
	public void testReverseInPlace() {
    int[] input2 = {1, 2, 3, 4};
    ArrayExamples.reverseInPlace(input2);
    assertArrayEquals(new int[] {4, 3, 2, 1}, input2);
	}
}
```
**Input does that passes JUnit test**
```
public class ArrayTests {
	@Test 
	public void testReverseInPlace() {
    int[] input1 = { 3 };
    ArrayExamples.reverseInPlace(input1);
    assertArrayEquals(new int[]{ 3 }, input1);
	}
}
```

As for the first input, we expected `{1}` as a return so it passed the test so JUnit did nit complain.

As for the second input, it failed the test as we expected to have `{4, 3, 2, 1}, so JUnit provides reason

![junit bug](https://user-images.githubusercontent.com/112384009/233771897-c5d3db97-c5f8-4122-8dc5-33140d605317.jpg)


* The bug here is how we use the **for loop** to write the method
```
for (int i = 0; i < arr.length; i += 1)
```
* The loops iterates through the whole array, when it reaches the middle and continue interating, the faulty output is produced.

* So here how we change the code (fix bug) so the method works as we expect
```
  // Changes the input array to be in reversed order
  static void reverseInPlace(int[] arr) {
    for(int i = 0; i < arr.length / 2; i++) {
        int temp = arr[i];
        arr[i] = arr[arr.length - i - 1];
        arr[arr.length - i - 1] = temp;
    }
  }
```

* And here is the result of testing the method (Both input 1 and input 2 are combined within one test)

![success test](https://user-images.githubusercontent.com/112384009/233772233-f0e36a18-7f1d-46f2-8462-ebeec7effb5e.jpg)

* The fix addresses the issue because the **for loop** only loops through half of the array, while creating a temp variable to store the element
of the list starting at index 0, then swaps that element with the element starting from the end of the list. Because the loop stops at the middle
of the array, we are sure that the elements from both halves are swapped.

## Part 3

In lab 2, I had a chance to practice with creating web server that I have not known before. In lab 3, I had a chance to work with some git command.\
Overall, lab 2 has much more to learn.
