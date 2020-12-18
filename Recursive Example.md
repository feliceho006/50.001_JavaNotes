## Recursive Implementation of atoi()
```java
class GFG{ 
// Recursive function to compute atoi() 
static int myAtoiRecursive(String str, int n) 
{   
    // Base case (Only one digit) 
    if (n == 1) 
    { return str.charAt(0) - '0'; } 
    // If more than 1 digits, recur for (n-1),  
    // multiplu result with 10 and add last digit 
    return (10 * myAtoiRecursive(str, n - 1) +  
                      str.charAt(n - 1) - '0'); 
} 
// Driver code 
public static void main(String[] s) 
{ 
    String str = "112"; 
    int n = str.length(); 
    System.out.println(myAtoiRecursive(str, n)); 
} 
} 
```
## Find all even length binary sequences with same sum of first and second half bits
```java
import java.io.*; 
import java.util.*; 
  
class GFG  
{ 
    // Function to print even length binary sequences 
    // whose sum of first and second half bits is same 
   
    // diff --> difference between sums of first n bits 
    // and last n bits 
    // out --> output array 
    // start --> starting index 
    // end --> ending index 
    static void findAllSequences(int diff, char out[],  
                                     int start, int end) 
    { 
        // We can't cover difference of more  
        // than n with 2n bits 
        if (Math.abs(diff) > (end - start + 1) / 2) 
            return; 
   
        // if all bits are filled 
        if (start > end) 
        { 
            // if sum of first n bits and 
            // last n bits are same 
            if (diff == 0) 
            { 
                System.out.print(out); 
                System.out.print(" "); 
            }     
            return; 
        } 
   
        // fill first bit as 0 and last bit as 1 
        out[start] = '0'; 
        out[end] = '1'; 
        findAllSequences(diff + 1, out, start + 1, end - 1); 
   
        // fill first and last bits as 1 
        out[start] = out[end] = '1'; 
        findAllSequences(diff, out, start + 1, end - 1); 
   
        // fill first and last bits as 0 
        out[start] = out[end] = '0'; 
        findAllSequences(diff, out, start + 1, end - 1); 
   
        // fill first bit as 1 and last bit as 0 
        out[start] = '1'; 
        out[end] = '0'; 
        findAllSequences(diff - 1, out, start + 1, end - 1); 
    } 
      
    // Driver program 
    public static void main (String[] args)  
    { 
        // input number 
        int n = 2; 
   
        // allocate string contaning 2*n characters 
        char[] out = new char[2 * n + 1]; 
   
        // null terminate output array 
        out[2 * n] = '\0'; 
   
        findAllSequences(0, out, 0, 2*n - 1); 
    } 
}
```
## Print all possible expressions that evaluate to a target
```java
static void check(double sum, double previous, String digits, double target, String expr) {
   if (digits.length() == 0) {
     if (sum + previous == target) {
       System.out.println(expr + " = " + target);
     }
   } else {
     for (int i = 1; i <= digits.length(); i++) {
       double current = Double.parseDouble(digits.substring(0, i));
       String remaining = digits.substring(i);
       check(sum + previous, current, remaining, target, expr + " + " + current);
       check(sum, previous * current, remaining, target, expr + " * " + current);
       check(sum, previous / current, remaining, target, expr + " / " + current);
       check(sum + previous, -current, remaining, target, expr + " - " + current);
     }
   }
 }

 static void f(String digits, double target) {
   for (int i = 1; i <= digits.length(); i++) {
     String current = digits.substring(0, i);
     check(0, Double.parseDouble(current), digits.substring(i), target, current);
   }
 } 
 ```
 ## Generate all binary strings without consecutive 1’s
 ```python
 def generateAllStringsUtil(K, str, n): 
      
    # print binary string without consecutive 1's 
    if (n == K): 
          
        # terminate binary string 
        print(*str[:n], sep = "", end = " ") 
        return
      
    # if previous character is '1' then we put 
    # only 0 at end of string 
    # example str = "01" then new string be "000" 
    if (str[n-1] == '1'): 
        str[n] = '0'
        generateAllStringsUtil (K, str, n + 1) 
          
    # if previous character is '0' than we put 
    # both '1' and '0' at end of string 
    # example str = "00" then new string "001" and "000" 
    if (str[n-1] == '0'): 
        str[n] = '0'
        generateAllStringsUtil(K, str, n + 1) 
        str[n] = '1'
        generateAllStringsUtil(K, str, n + 1)  
          
# function generate all binary string without 
# consecutive 1's 
def generateAllStrings(K): 
      
    # Base case 
    if (K <= 0): 
        return
      
    # One by one stores every binary string of length K 
    str = [0] * K 
      
    # Generate all Binary string starts with '0' 
    str[0] = '0'
    generateAllStringsUtil (K, str, 1)  
      
    # Generate all Binary string starts with '1' 
    str[0] = '1'
    generateAllStringsUtil (K, str, 1) 
  
# Driver code 
K = 3
generateAllStrings (K)
```
## Recursive solution to count substrings with same first and last characters
```java
class GFG 
{ 
    // Function to count subtrings 
    // with same first and  
    // last characters 
    static int countSubstrs(String str, int i,  
                                         int j, int n) 
    { 
        // base cases 
        if (n == 1) 
            return 1; 
        if (n <= 0) 
            return 0; 
      
        int res = countSubstrs(str, i + 1, j, n - 1) +  
                countSubstrs(str, i, j - 1, n - 1) - 
                countSubstrs(str, i + 1, j - 1, n - 2);          
      
        if (str.charAt(i) == str.charAt(j)) 
            res++;  
      
        return res; 
    } 
      
    // Driver code 
    public static void main (String[] args) 
    { 
        String str = "abcab"; 
        int n = str.length(); 
        System.out.print(countSubstrs(str, 0, n - 1, n)); 
    } 
}
```
## All possible binary numbers of length n with equal sum in both halves
```java
import java.util.*; 
  
class GFG 
{ 
  
// Default values are used only in initial call. 
// n is number of bits remaining to be filled 
// di is current difference between sums of 
// left and right halves. 
// left and right are current half substrings.  
static void equal(int n, String left,  
                         String right, int di) 
{ 
    // TWO BASE CASES 
    // If there are no more characters to add (n is 0) 
    if (n == 0) 
    { 
        // If difference between counts of 1s and 
        // 0s is 0 (di is 0) 
        if (di == 0) 
            System.out.print(left + right + " "); 
        return; 
    } 
  
    /* If 1 remains than string length was odd */
    if (n == 1) 
    { 
        // If difference is 0, we can put  
        // remaining bit in middle. 
        if (di == 0) 
        { 
            System.out.print(left + "0" + right + " "); 
            System.out.print(left + "1" + right + " "); 
        } 
        return; 
    } 
  
    /* If difference is more than what can be 
    be covered with remaining n digits 
    (Note that lengths of left and right 
     must be same) */
    if ((2 * Math.abs(di) <= n)) 
    { 
          
            // add 0 to end in both left and right 
            // half. Sum in both half will not 
            // change 
            equal(n - 2, left + "0", right + "0", di); 
  
            // add 0 to end in both left and right 
            // half* subtract 1 from di as right 
            // sum is increased by 1 
            equal(n - 2, left + "0", right + "1", di - 1); 
          
  
        // add 1 in end in left half and 0 to the 
        // right half. Add 1 to di as left sum is 
        // increased by 1* 
        equal(n - 2, left + "1", right + "0", di + 1); 
  
        // add 1 in end to both left and right 
        // half the sum will not change 
        equal(n - 2, left + "1", right + "1", di); 
    } 
} 
  
// Driver Code 
public static void main(String args[]) 
{ 
    int n = 5;  
      
    // n-bits 
    equal(n, "", "", 0); 
} 
}
```
## Combinations in a String of Digits
```java
class GFG 
{ 
      
// function to print combinations of numbers  
// in given input string 
static void printCombinations(char[] input, 
                              int index,  
                              char[] output,  
                              int outLength) 
{ 
    // no more digits left in input string 
    if (input.length == index) 
    { 
        // print output string & return 
        System.out.println(String.valueOf(output)); 
        return; 
    } 
      
    // place current digit in input string 
    output[outLength] = input[index]; 
      
    // separate next digit with a space 
    output[outLength + 1] = ' '; 
      
    printCombinations(input, index + 1, output,  
                                outLength + 2); 
      
    // if next digit exists make a  
    // call without including space 
    if(input.length!=index + 1) 
    printCombinations(input, index + 1, output,  
                                outLength + 1); 
} 
  
// Driver Code 
public static void main(String[] args)  
{ 
    char input[] = "1214".toCharArray(); 
    char []output = new char[100]; 
      
    printCombinations(input, 0, output, 0); 
} 
}
```
## Count consonants in a string (Iterative and recursive methods)
```java
import java.io.*; 
  
class GFG { 
  
    // Function to check for consonant 
    static boolean isConsonant(char ch) 
    { 
        // To handle lower case 
        ch = Character.toUpperCase(ch); 
       
        return !(ch == 'A' || ch == 'E' ||  
                ch == 'I' || ch == 'O' ||  
                ch == 'U') && ch >= 65 && ch <= 90; 
    } 
   
    static int totalConsonants(String str) 
    { 
        int count = 0; 
        for (int i = 0; i < str.length(); i++)  
       
            // To check is character is Consonant 
            if (isConsonant(str.charAt(i))) 
                ++count; 
        return count; 
    } 
      
    // Driver code 
    public static void main(String args[]) 
    { 
        String str = "abc de"; 
        System.out.println( totalConsonants(str)); 
    } 
} 
```
## Program for length of a string using recursion
```java
import java.util.*; 
  
public class GFG{ 
  
    /* Function to calculate length */
    private static int recLen(String str)  
    { 
  
        // if we reach at the end of the string 
        if (str.equals("")) 
            return 0; 
        else
            return recLen(str.substring(1)) + 1; 
    } 
  
    /* Driver program to test above function */
    public static void main(String[] args)  
    { 
  
          
        String str ="GeeksforGeeks"; 
        System.out.println(recLen(str)); 
    } 
} 
```
## First uppercase letter in a string (Iterative and Recursive)
```java
import java.io.*; 
import java.util.*; 
  
class GFG { 
  
    // Function to find string which has 
    // first character of each word. 
    static char first(String str) 
    { 
        for (int i = 0; i < str.length(); i++) 
            if (Character.isUpperCase(str.charAt(i))) 
                return str.charAt(i); 
        return 0; 
    } 
      
    // Driver program  
    public static void main(String args[]) 
    { 
        String str = "geeksforGeeKS"; 
        char res = first(str); 
        if (res == 0) 
            System.out.println("No uppercase letter"); 
        else
            System.out.println(res); 
    } 
}
```
## Partition given string in such manner that i’th substring is sum of (i-1)’th and (i-2)’th substring
```java
import java.util.LinkedList; 
  
public class SumArray { 
  
  private static LinkedList<Integer> resultList =  
                                   new LinkedList<>(); 
  
  private static boolean check(char[] chars, int offset1,  
       int offset2, int offset3, boolean freezeFirstAndSecond) { 
  
    // Find subarrays according to given offsets 
    int first = intOf(subArr(chars, 0, offset1)); 
    int second = intOf(subArr(chars, offset1, offset2)); 
    int third = intOf(subArr(chars, offset1 + offset2, offset3)); 
  
    // If condition is satisfied for current subarrays 
    if (first + second == third) { 
  
      // If whole array is covered. 
      if (offset1 + offset2 + offset3 >= chars.length) { 
        resultList.add(first); 
        resultList.add(second); 
        resultList.add(third); 
        return true; 
      } 
        
      // Check if remaining array also satisfies the condition 
      boolean result = check(subArr(chars, offset1,  
           chars.length - offset1), offset2, offset3, 
                  Math.max(offset2, offset3), true); 
      if (result) { 
        resultList.addFirst(first); 
      } 
      return result; 
    } 
  
    // If not satisfied, try incrementing third 
    if (isValidOffSet(offset1, offset2, 1 + offset3, chars.length)) { 
      if (check(chars, offset1, offset2, 1 + offset3, false))  
        return true;       
    } 
  
    // If first and second have been finalized, do not  
    // alter already computed results 
    if (freezeFirstAndSecond) 
      return false; 
   
    // If first and second are not finalized 
    if (isValidOffSet(offset1, 1 + offset2, Math.max(offset1,  
                           1 + offset2),  chars.length)) { 
  
      // Try incrementing second 
      if (check(chars, offset1, 1 + offset2, 
           Math.max(offset1, 1 + offset2), false))  
        return true;       
    } 
  
    // Try incrementing first 
    if (isValidOffSet(1 + offset1, offset2, Math.max(1 + offset1, 
                                  offset2),  chars.length)) { 
     if (check(chars, 1 + offset1, offset2, Math.max(1 + offset1, 
                                             offset2), false))  
        return true; 
    } 
    return false; 
  } 
  
  // Check if given three offsets are valid (Within array length 
  // and third offset can represent sum of first two) 
  private static boolean isValidOffSet(int offset1, int offset2,  
                                   int offset3, int length) { 
    return (offset1 + offset2 + offset3 <= length && 
            (offset3 == Math.max(offset1, offset2) || 
             offset3 == 1 + Math.max(offset1, offset2))); 
  } 
  
  // To get a subarray with starting from given  
  // index and offset 
  private static char[] subArr(char[] chars, int index, int offset) { 
    int trueOffset = Math.min(chars.length - index, offset); 
    char[] destArr = new char[trueOffset]; 
    System.arraycopy(chars, index, destArr, 0, trueOffset); 
    return destArr; 
  } 
  
  private static int intOf(char... chars) { 
    return Integer.valueOf(new String(chars)); 
  } 
  
  public static void main(String[] args) { 
    String numStr = "11235813"; 
    char[] chars = numStr.toCharArray(); 
    System.out.println(check(chars, 1, 1, 1, false)); 
    System.out.println(resultList); 
  } 
} 
```
## Power Set in Lexicographic order
```java
import java.util.*; 
  
class GFG { 
  
    // str : Stores input string 
    // n : Length of str. 
    // curr : Stores current permutation 
    // index : Index in current permutation, curr 
    static void permuteRec(String str, int n, 
                           int index, String curr) 
    { 
        // base case 
        if (index == n) { 
            return; 
        } 
        System.out.println(curr); 
        for (int i = index + 1; i < n; i++) { 
  
            curr += str.charAt(i); 
            permuteRec(str, n, i, curr); 
  
            // backtracking 
            curr = curr.substring(0, curr.length() - 1); 
        } 
        return; 
    } 
  
    // Generates power set in lexicographic 
    // order. 
    static void powerSet(String str) 
    { 
        char[] arr = str.toCharArray(); 
        Arrays.sort(arr); 
        permuteRec(new String(arr), str.length(), -1, ""); 
    } 
  
    // Driver code 
    public static void main(String[] args) 
    { 
        String str = "cab"; 
        powerSet(str); 
    } 
} 
```
## Function to copy string (Iterative and Recursive)
```java
class GFG 
{ 
      
// Function to copy one string to other 
// assuming that other string has enough 
// space. 
static void myCopy(char s1[], char s2[]) 
{ 
    int i = 0; 
    for (i = 0; i < s1.length; i++) 
         s2[i] = s1[i]; 
} 
  
// Driver code 
public static void main(String[] args)  
{ 
    char s1[] = "GEEKSFORGEEKS".toCharArray(); 
    char s2[] = new char[s1.length]; 
    myCopy(s1, s2); 
    System.out.println(String.valueOf(s2)); 
} 
} 
```
## Print all increasing sequences of length k from first n natural numbers
```java
class GFG { 
      
    // A utility function to print  
    // contents of arr[0..k-1] 
    static void printArr(int[] arr, int k) 
    { 
        for (int i = 0; i < k; i++) 
            System.out.print(arr[i] + " "); 
        System.out.print("\n"); 
    } 
      
    // A recursive function to print 
    // all increasing sequences 
    // of first n natural numbers.  
    // Every sequence should be 
    // length k. The array arr[] is  
    // used to store current sequence 
    static void printSeqUtil(int n, int k,  
                             int len, int[] arr) 
    { 
          
        // If length of current increasing 
        // sequence becomes k, print it 
        if (len == k) 
        { 
            printArr(arr, k); 
            return; 
        } 
      
        // Decide the starting number  
        // to put at current position: 
        // If length is 0, then there 
        // are no previous elements 
        // in arr[]. So start putting  
        // new numbers with 1. 
        // If length is not 0,  
        // then start from value of 
        // previous element plus 1. 
        int i = (len == 0) ? 1 : arr[len - 1] + 1; 
      
        // Increase length 
        len++; 
      
        // Put all numbers (which are  
        // greater than the previous 
        // element) at new position. 
        while (i <= n) 
        { 
            arr[len - 1] = i; 
            printSeqUtil(n, k, len, arr); 
            i++; 
        } 
      
        // This is important. The  
        // variable 'len' is shared among 
        // all function calls in recursion  
        // tree. Its value must be 
        // brought back before next  
        // iteration of while loop 
        len--; 
    } 
      
    // This function prints all  
    // increasing sequences of 
    // first n natural numbers.  
    // The length of every sequence 
    // must be k. This function 
    // mainly uses printSeqUtil() 
    static void printSeq(int n, int k) 
    { 
          
        // An array to store  
        // individual sequences 
        int[] arr = new int[k]; 
          
        // Initial length of  
        // current sequence 
        int len = 0;  
        printSeqUtil(n, k, len, arr); 
    } 
  
    // Driver Code 
    static public void main (String[] args) 
    { 
        int k = 3, n = 7; 
        printSeq(n, k); 
    } 
} 
```
## Generate all possible sorted arrays from alternate elements of two given sorted arrays
```java
class GenerateArrays { 
  
    /* Function to generates and prints all sorted arrays from alternate 
       elements of 'A[i..m-1]' and 'B[j..n-1]' 
       If 'flag' is true, then current element is to be included from A  
       otherwise from B. 
       'len' is the index in output array C[]. We print output array   
       each time before including a character from A only if length of  
       output array is greater than 0. We try than all possible  
       combinations */
    void generateUtil(int A[], int B[], int C[], int i, int j, int m, int n, 
            int len, boolean flag)  
    { 
        if (flag) // Include valid element from A 
        { 
            // Print output if there is at least one 'B' in output array 'C' 
            if (len != 0)  
                printArr(C, len + 1); 
  
            // Recur for all elements of A after current index 
            for (int k = i; k < m; k++)  
            { 
                if (len == 0)  
                { 
                    /* this block works for the very first call to include 
                    the first element in the output array */
                    C[len] = A[k]; 
  
                    // don't increment lem as B is included yet 
                    generateUtil(A, B, C, k + 1, j, m, n, len, !flag); 
                }  
                  
                /* include valid element from A and recur */
                else if (A[k] > C[len])  
                { 
                        C[len + 1] = A[k]; 
                        generateUtil(A, B, C, k + 1, j, m, n, len + 1, !flag); 
                } 
            } 
        }  
          
        /* Include valid element from B and recur */
        else
        { 
            for (int l = j; l < n; l++)  
            { 
                if (B[l] > C[len])  
                { 
                    C[len + 1] = B[l]; 
                    generateUtil(A, B, C, i, l + 1, m, n, len + 1, !flag); 
                } 
            } 
        } 
    } 
  
    /* Wrapper function */
    void generate(int A[], int B[], int m, int n)  
    { 
        int C[] = new int[m + n]; 
       
        /* output array */
        generateUtil(A, B, C, 0, 0, m, n, 0, true); 
    } 
  
    // A utility function to print an array 
    void printArr(int arr[], int n)  
    { 
        for (int i = 0; i < n; i++) 
            System.out.print(arr[i] + " "); 
        System.out.println(""); 
    } 
  
    public static void main(String[] args)  
    { 
        GenerateArrays generate = new GenerateArrays(); 
        int A[] = {10, 15, 25}; 
        int B[] = {5, 20, 30}; 
        int n = A.length; 
        int m = B.length; 
        generate.generate(A, B, n, m); 
    } 
}
```
## Program to find the minimum (or maximum) element of an array
```java
class GFG 
{
 
static int getMin(int arr[], int i, int n)
{
    // If there is single element, return it.
    // Else return minimum of first element and
    // minimum of remaining array.
    return (n == 1) ? arr[i] : Math.min(arr[i], 
                        getMin(arr,i + 1 , n - 1));
}
 
static int getMax(int arr[], int i, int n)
{
    // If there is single element, return it.
    // Else return maximum of first element and
    // maximum of remaining array.
    return (n == 1) ? arr[i] : Math.max(arr[i], 
                         getMax(arr ,i + 1, n - 1));
}
 
// Driver code
public static void main(String[] args) 
{
    int arr[] = { 12, 1234, 45, 67, 1 };
    int n = arr.length;
    System.out.print("Minimum element of array: " + 
                        getMin(arr, 0, n) + "\n");
    System.out.println("Maximum element of array: " + 
                        getMax(arr, 0, n));
    }
}
```
## Sum triangle from array
```java
import java.util.*; 
import java.lang.*; 
  
public class ConstructTriangle 
{ 
    // Function to generate Special Triangle. 
    public static void printTriangle(int[] A) 
    { 
        // Base case 
        if (A.length < 1) 
            return; 
  
        // Creating new array which contains the 
        // Sum of consecutive elements in 
        // the array passes as parameter. 
        int[] temp = new int[A.length - 1]; 
        for (int i = 0; i < A.length - 1; i++) 
        { 
            int x = A[i] + A[i + 1]; 
            temp[i] = x; 
        } 
  
        // Make a recursive call and pass 
        // the newly created array 
        printTriangle(temp); 
  
        // Print current array in the end so 
        // that smaller arrays are printed first 
        System.out.println(Arrays.toString(A)); 
    } 
  
    // Driver function 
    public static void main(String[] args) 
    { 
        int[] A = { 1, 2, 3, 4, 5 }; 
        printTriangle(A); 
    } 
} 
```
## Recursive function to delete k-th node from linked list
```java
class GFG 
{ 
      
static class Node  
{  
    int data;  
    Node next;  
};  
  
// Deletes k-th node and returns new header.  
static Node deleteNode(Node start, int k)  
{  
    // If invalid k  
    if (k < 1)  
    return start;  
  
    // If linked list is empty  
    if (start == null)  
    return null;  
  
    // Base case (start needs to be deleted)  
    if (k == 1)  
    {  
        Node res = start.next;  
        return res;  
    }  
      
    start.next = deleteNode(start.next, k-1);  
    return start;  
}  
  
// Utility function to insert a node at the beginning / 
static Node push( Node head_ref, int new_data)  
{  
    Node new_node = new Node();  
    new_node.data = new_data;  
    new_node.next = head_ref;  
    head_ref = new_node;  
    return head_ref; 
}  
  
// Utility function to print a linked list / 
static void printList( Node head)  
{  
    while (head!=null)  
    {  
        System.out.print(head.data + " ");  
        head = head.next;  
    }  
    System.out.printf("\n");  
}  
  
// Driver program to test above functions / 
public static void main(String args[]) 
{  
    Node head = null;  
  
    // Create following linked list  
    //12.15.10.11.5.6.2.3 / 
    head=push(head,3);  
    head=push(head,2);  
    head=push(head,6);  
    head=push(head,5);  
    head=push(head,11);  
    head=push(head,10);  
    head=push(head,15);  
    head=push(head,12);  
      
    int k = 3;  
    head = deleteNode(head, k);  
  
    System.out.printf("\nModified Linked List: ");  
    printList(head);  
} 
}
```
## Recursive insertion and traversal linked list
```java
class GFG 
{ 
      
static class Node  
{  
    int data;  
    Node next;  
};  
  
// Allocates a new node with given data  
static Node newNode(int data)  
{  
    Node new_node = new Node();  
    new_node.data = data;  
    new_node.next = null;  
    return new_node;  
}  
  
// Function to insert a new node at the  
// end of linked list using recursion.  
static Node insertEnd(Node head, int data)  
{  
    // If linked list is empty, create a  
    // new node (Assuming newNode() allocates  
    // a new node with given data)  
    if (head == null)  
        return newNode(data);  
  
    // If we have not reached end, keep traversing  
    // recursively.  
    else
        head.next = insertEnd(head.next, data);  
    return head;  
}  
  
static void traverse(Node head)  
{  
    if (head == null)  
    return;  
      
    // If head is not null, print current node  
    // and recur for remaining list  
    System.out.print( head.data + " ");  
  
    traverse(head.next);  
}  
  
// Driver code  
public static void main(String args[]) 
{  
    Node head = null;  
    head = insertEnd(head, 6);  
    head = insertEnd(head, 8);  
    head = insertEnd(head, 10);  
    head = insertEnd(head, 12);  
    head = insertEnd(head, 14);  
    traverse(head);  
}  
} 
```
## Reverse a Doubly linked list using recursion
```java
class GFG 
{ 
      
// a node of the doubly linked list  
static class Node  
{  
    int data;  
    Node next, prev;  
};  
  
// function to get a new node  
static Node getNode(int data)  
{  
    // allocate space  
    Node new_node = new Node();  
    new_node.data = data;  
    new_node.next = new_node.prev = null;  
    return new_node;  
}  
  
// function to insert a node at the beginning  
// of the Doubly Linked List  
static Node push(Node head_ref, Node new_node)  
{  
    // since we are adding at the beginning,  
    // prev is always null  
    new_node.prev = null;  
  
    // link the old list off the new node  
    new_node.next = (head_ref);  
  
    // change prev of head node to new node  
    if ((head_ref) != null)  
        (head_ref).prev = new_node;  
  
    // move the head to point to the new node  
    (head_ref) = new_node;  
    return head_ref; 
}  
  
// function to reverse a doubly linked list  
static Node Reverse(Node node)  
{  
    // If empty list, return  
    if (node == null)  
        return null;  
  
    // Otherwise, swap the next and prev  
    Node temp = node.next;  
    node.next = node.prev;  
    node.prev = temp;  
  
    // If the prev is now null, the list  
    // has been fully reversed  
    if (node.prev == null)  
        return node;  
  
    // Otherwise, keep going  
    return Reverse(node.prev);  
}  
  
// Function to print nodes in a given doubly  
// linked list  
static void printList(Node head)  
{  
    while (head != null) 
    {  
        System.out.print( head.data + " ");  
        head = head.next;  
    }  
}  
  
// Driver code  
public static void main(String args[])  
{  
    // Start with the empty list  
    Node head = null;  
  
    // Create doubly linked: 10<.8<.4<.2 /  
    head = push(head, getNode(2));  
    head = push(head, getNode(4));  
    head = push(head, getNode(8));  
    head = push(head, getNode(10));  
    System.out.print( "Original list: ");  
    printList(head);  
  
    // Reverse doubly linked list  
    head = Reverse(head);  
    System.out.print("\nReversed list: ");  
    printList(head);  
}  
} 
```
## Delete a linked list using recursion
```java
class GFG  
{ 
  
/* Link list node */
static class Node  
{ 
    int data; 
    Node next; 
}; 
  
/* Recursive Function to delete 
the entire linked list */
static void deleteList(Node head) 
{ 
    if (head == null) 
        return; 
    deleteList(head.next);  
    System.gc(); 
} 
  
/* Given a reference (pointer to pointer) to  
the head of a list and an int, push a new 
node on the front of the list. */
static void push(Node head_ref, int new_data) 
{ 
    Node new_node = new Node(); 
    new_node.data = new_data; 
    new_node.next = head_ref; 
    head_ref = new_node; 
} 
  
/* Driver code*/
public static void main(String[] args)  
{ 
    /* Start with the empty list */
    Node head = new Node(); 
  
    /* Use push() to conbelow list 
    1->12->1->4->1 */
    push(head, 1); 
    push(head, 4); 
    push(head, 1); 
    push(head, 12); 
    push(head, 1); 
    System.out.print("\nDeleting linked list"); 
    deleteList(head); 
    System.out.print("\nLinked list deleted"); 
} 
} 
```
## Print alternate nodes of a linked list using recursion
```java
class GFG  
{ 
  
// A linked list node  
static class Node  
{  
    int data;  
    Node next;  
};  
  
// Inserting node at the beginning  
static Node push( Node head_ref, int new_data)  
{  
    Node new_node = new Node();  
    new_node.data = new_data;  
    new_node.next = (head_ref);  
    (head_ref) = new_node;  
    return head_ref; 
}  
  
// Function to print alternate nodes of linked list.  
// The boolean flag isOdd is used to find if the current  
// node is even or odd.  
static void printAlternate( Node node, boolean isOdd)  
{  
    if (node == null)  
    return;  
    if (isOdd == true)  
        System.out.print( node.data + " ");  
    printAlternate(node.next, !isOdd);  
}  
  
// Driver code  
public static void main(String args[]) 
{  
    // Start with the empty list  
    Node head = null;  
  
    // con below list  
    // 1.2.3.4.5.6.7.8.9.10  
  
    head = push(head, 10);  
    head = push(head, 9);  
    head = push(head, 8);  
    head = push(head, 7);  
    head = push(head, 6);  
    head = push(head, 5);  
    head = push(head, 4);  
    head = push(head, 3);  
    head = push(head, 2);  
    head = push(head, 1);  
  
    printAlternate(head,true);  
  
} 
}
```
## Recursive approach for alternating split of Linked List
```java
class GFG 
{ 
      
// Node structure 
static class Node  
{ 
    int data; 
    Node next; 
}; 
  
// Function to push nodes 
// into linked list 
static Node push(Node head, int new_data) 
{ 
    Node new_node = new Node(); 
    new_node.data = new_data; 
    new_node.next = (head); 
    (head) = new_node; 
    return head; 
} 
  
static Node a = null, b = null; 
  
// We basically remove link between 'a' 
// and its next. Similarly we remove link 
// between 'b' and its next. Then we recur 
// for remaining lists. 
static void moveNode(Node a, Node b) 
{ 
    if (b == null || a == null) 
        return; 
  
    if (a.next != null) 
        a.next = a.next.next; 
  
    if (b.next != null) 
        b.next = b.next.next; 
  
    moveNode(a.next, b.next); 
} 
  
// function to split linked list 
static void alternateSplitLinkedList(Node head) 
{ 
    Node curr = head; 
    a = curr; 
    b = curr.next; 
    Node aRef = a, bRef = b; 
    moveNode(aRef, bRef); 
} 
  
static void display(Node head) 
{ 
    Node curr = head; 
    while (curr != null)  
    { 
        System.out.printf("%d ", curr.data); 
        curr = curr.next; 
    } 
} 
  
// Driver code 
public static void main(String args[]) 
{ 
    Node head = null;  
    head = push(head, 7); 
    head = push(head, 6); 
    head = push(head, 5); 
    head = push(head, 4); 
    head = push(head, 3); 
    head = push(head, 2); 
    head = push(head, 1); 
      
    alternateSplitLinkedList(head); 
  
    System.out.printf("a : "); 
    display(a); 
    System.out.printf("\nb : "); 
    display(b); 
} 
}
```
## Find middle of singly linked list Recursively
```java
class GFG 
{ 
  
// Tree Node Structure  
static class Node  
{  
    int data;  
    Node next;  
};  
  
// Create new Node  
static Node newLNode(int data)  
{  
    Node temp = new Node();  
    temp.data = data;  
    temp.next = null;  
    return temp;  
}  
  
static int n; 
static Node mid; 
  
// Function for finding midpoint recursively  
static void midpoint_util(Node head )  
{  
  
    // If we reached end of linked list  
    if (head == null)  
    {  
        n = (n) / 2;  
        return;  
    }  
  
    n = n + 1;  
  
    midpoint_util(head.next);  
  
    // Rolling back, decrement n by one  
    n = n - 1;  
    if (n == 0)  
    {  
  
        // Final answer  
        mid = head;  
    }  
}  
  
static Node midpoint(Node head)  
{  
    mid = null;  
    n = 1;  
    midpoint_util(head);  
    return mid;  
}  
  
// Driver code 
public static void main(String args[]) 
{  
    Node head = newLNode(1);  
    head.next = newLNode(2);  
    head.next.next = newLNode(3);  
    head.next.next.next = newLNode(4);  
    head.next.next.next.next = newLNode(5);  
    Node result = midpoint(head);  
    System.out.print( result.data );  
} 
}
```