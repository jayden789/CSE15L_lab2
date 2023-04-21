# Lab 2 Report: Servers and Bugs
## Part 1
Code for **StringServer** and **/add-message**


![StringServer](https://user-images.githubusercontent.com/112384009/233736845-6a1784ae-2025-488f-bba7-e1ca5ae46c78.jpg)

`add-message?s=Friday`

![friday](https://user-images.githubusercontent.com/112384009/233737227-8f83ba79-7b5e-42b1-9f53-b2b1eb1324fe.jpg)

* The method called is `String handleRequest(URI url)`, it return a String object, which is what we want to print on screen,
also there are some other methods being called like `getPath()`, `contains()`, `equals()`, `getQuery()`...

What are the relevant arguments to those methods, and the values of any relevant fields of the class?
* The `**String handleRequest(URI url)**` need an url (which is `http://localhost:4000/add-message?s=Friday`
object to process our request, look for the path to check for certain things.
If the path contains `/add-message`, then it will filter the query (which starts after **?**) and print out the string we give.
In this example, we the intial string is an empty string, and we give query ( after the `**?**`) `s=Friday`.

How do the values of any relevant fields of the class change from this specific request? If no values got changed, explain why.


`add-message?s=Saturday`

![sat](https://user-images.githubusercontent.com/112384009/233737263-16f1c63f-00fc-4377-9f6b-44d9d4c4d91a.jpg)

Which methods in your code are called?
* The method called is ` String handleRequest(URI url)`, it return a String object, which is what we want to print on screen
What are the relevant arguments to those methods, and the values of any relevant fields of the class?
How do the values of any relevant fields of the class change from this specific request? If no values got changed, explain why.
