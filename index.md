# Part 1

-String Server code:

![Image](stringserver1.png)
![Image](stringserver2.png)

-StringServer First Output:

![Image](hello.png)

- Method `handle`is called(in the class `MyHandler`)
- The values of the class fields are:
  * `HttpExchange t = localhost:17/add-message?s=hello`
  * `URI uri = add-message?s=hello` took the path from `localhost:27/add-message?s=hello`
  * `String query = s=hello` query from `add-message?s=hello`
  * `String[] keyValue = keyValue[0] = s, keyValue[1] = hello` -seperated `s` from `hello`
  * `message = hello -returned \n + keyValue[1]`
  * `response = hello` -copied the value of `message` into `response`


-StringServer Second Output:

![Image](how are you.png)

- Method `handle`is called(in the class `MyHandler`)
- The values of the class fields are:
  * `HttpExchange t = localhost:17/add-message?s=how are you?`
  * `URI uri = add-message?s=how are you?` took the path from `localhost:27/add-message?s=how are you?`
  * `String query = s=how are you?` query from `add-message?s=how are you?`
  * `String[] keyValue = keyValue[0] = s, keyValue[1] = how are you?` -seperated `s` from `how are you?`
  * `message = hello -\nhow are yo?` added as well `\n + keyValue[1]` to `hello`
  * `response = hello \nhow are you?` copied the value of `message` to `repsonse`
  
  
  # Part 2

-The bug I will be going through from this lab is from the method reverseInPlace(int[] arr).The given method reverseInPlace takes 
an array of integers arr as input and modifies the input array by reversing its elements in place.

-Failure-inducing input:
```
public void testReverseInPlaceFailure() {
    int[] arr = {1, 2, 3, 4, 5};
    reverseInPlace(arr);
    assertArrayEquals(new int[]{5, 4, 3, 2, 1}, arr);
}
```
The test output would have the array differed at element[3], where the expected value would be 2 but was 4 instead. The reason for this is because the original code does not reverse the elements of the array, but instead overwrites each element with the value at the corresponding position from the end of the array.

-Non-failure input:
```
public void testReverseInPlaceNoFailure() {
    int[] arr = {1, 2, 3};
    reverseInPlace(arr);
    assertArrayEquals(new int[]{3, 2, 1}, arr);
}
```

![Image](failure.png)
-The problem with the failure-inducing input was that the method ran where it ended up overwriting each element of the array with the value at the corresponding position from the end of the array(instead of reverseing the elements).

![Image](non-failure.png)
-Here the non-failure input correctly passes the tester.
Here with this input, the method correctly 

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

# Part 3

One thing I learned from lab in week 2/3 was changing the though process on finding bugs. Before I would just randomly change my code and see if it would work. But after reading the lecture articles and going through the lab steps I was able to gain a new mindset where I have a much more clear thought process with lookiing through the code for a bug that was messing up my program.
