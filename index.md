# Part 1

-String Server code:

![Image](StringServerCode.png)

-StringServer First Output:

![Image](output1.png)

- Method `handle`is called(in the class `MyHandler`)
- The values of the class fields are:
  * `HttpExchange t = localhost:17/add-message?s=hello`
  * `URI uri = add-message?s=hello` took the path from `localhost:27/add-message?s=hello`
  * `String query = s=hello` query from `add-message?s=hello`
  * `String[] keyValue = keyValue[0] = s, keyValue[1] = hello` -seperated `s` from `hello`
  * `message = hello -returned \n + keyValue[1]`
  * `response = hello` -copied the value of `message` into `response`


-StringServer Second Output:

![Image](output2.png)

- Method `handle`is called(in the class `MyHandler`)
- The values of the class fields are:
  * `HttpExchange t = localhost:17/add-message?s=how are you?`
  * `URI uri = add-message?s=how are you?` took the path from `localhost:27/add-message?s=how are you?`
  * `String query = s=how are you?` query from `add-message?s=how are you?`
  * `String[] keyValue = keyValue[0] = s, keyValue[1] = how are you?` -seperated `s` from `how are you?`
  * `message = hello -\nhow are yo?` added as well `\n + keyValue[1]` to `hello`
  * `response = hello \nhow are you?` copied the value of `message` to `repsonse`
  
  
  # Part 2

-The bug I will be going through from this lab is from the method reverseInPlace(int[] arr)

-Failure-inducing input:
```
public void testReverseInPlaceFailure() {
    int[] arr = {1, 2, 3, 4, 5};
    reverseInPlace(arr);
    assertArrayEquals(new int[]{5, 4, 3, 2, 1}, arr);
}
```

-Non-failure input:
```
public void testReverseInPlaceNoFailure() {
    int[] arr = {1, 2, 3};
    reverseInPlace(arr);
    assertArrayEquals(new int[]{3, 2, 1}, arr);
}
```
Bug fix:
 -Original code:
 ```
 static void reverseInPlace(int[] arr) {
    for(int i = 0; i < arr.length; i += 1) {
      arr[i] = arr[arr.length - i - 1];
    }
  ```
  
  -Fixed Code:
  ```
  static void reverseInPlace(int[] arr) {
    for(int i = 0; i < arr.length / 2; i += 1) {
        int temp = arr[i];
        arr[i] = arr[arr.length - i - 1];
        arr[arr.length - i - 1] = temp;
    }
}
```

The fixed code addresses the issue by using a temp variable to swap the elements in place so that the array is reversed correctly. The problem with the first version of the code was that it overwrote each element of the array with the corresponding element from the end.

# Part 3

One thing I learned from lab in week 2/3 was changing the though process on finding bugs. Before I would just randomly change my code and see if it would work. But after reading the lecture articles and going through the lab steps I was able to gain a new mindset where I have a much more clear thought process with lookiing through the code for a bug that was messing up my program.
