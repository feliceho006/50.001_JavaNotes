## Print a pattern without using any loop
```java
import java.io.*; 
  
class GFG { 
      
    // Recursive function to print the pattern. 
    // n indicates input value 
    // m indicates current value to be printed 
    // flag indicates whether we need to add 5 or 
    // subtract 5. Initially flag is true. 
    static void printPattern(int n, int m, boolean flag) 
    { 
          
        // Print m. 
        System.out.print(m + " "); 
  
        // If we are moving back toward the n and 
        // we have reached there, then we are done 
        if (flag == false && n == m) 
            return; 
  
        // If we are moving toward 0 or negative. 
        if (flag) { 
  
            // If m is greater, then 5, recur with  
            // true flag 
            if (m - 5 > 0) 
                printPattern(n, m - 5, true); 
  
            else // recur with false flag 
                printPattern(n, m - 5, false); 
        } 
  
        else // If flag is false. 
            printPattern(n, m + 5, false); 
    } 
  
    // Driver Program 
    public static void main(String[] args) 
    { 
        int n = 16; 
        printPattern(n, n, true); 
    } 
}
```
## Print all non-increasing sequences of sum equal to a given number x
```java
class GFG {
     
    // Utility function to print array
    // arr[0..n-1]
    static void printArr(int arr[], int n)
    {
        for (int i = 0; i < n; i++)
            System.out.printf("%d ", arr[i]);
             
        System.out.println("");
    }
     
    // Recursive Function to generate all 
    // non-increasing sequences with sum x
    // arr[] --> Elements of current sequence
    // curr_sum --> Current Sum
    // curr_idx --> Current index in arr[]
    static void generateUtil(int x, int arr[],
                     int curr_sum, int curr_idx)
    {
         
        // If current sum is equal to x, then
        // we found a sequence
        if (curr_sum == x)
        {
            printArr(arr, curr_idx);
            return;
        }
         
        // Try placing all numbers from 1 to 
        // x-curr_sum at current index
        int num = 1;
         
        // The placed number must also be 
           // smaller than previously placed
           // numbers and it may be equal to 
           // the previous stored value, i.e.,
           // arr[curr_idx-1] if there exists
           // a pevious number
        while (num <= x - curr_sum && 
                             (curr_idx == 0 ||
                     num <= arr[curr_idx - 1]))
        {
             
            // Place number at curr_idx
            arr[curr_idx] = num;
         
            // Recur
            generateUtil(x, arr, curr_sum+num,
                                     curr_idx + 1);
         
            // Try next number
            num++;
        }
    }
     
    // A wrapper over generateUtil()
    static void generate(int x)
    {
         
        // Array to store sequences on by one
        int arr[] = new int [x];
        generateUtil(x, arr, 0, 0);
    }
     
    // Driver program
    public static void main(String[] args)
    {
        int x = 5;
        generate(x);
    }
}
```
## Print all n-digit strictly increasing numbers
```java
import java.io.*; 
  
class Increasing 
{ 
    // Function to print all n-digit numbers whose digits 
    // are strictly increasing from left to right. 
    // out   --> Stores current output number as string 
    // start --> Current starting digit to be considered 
    void findStrictlyIncreasingNum(int start, String out, int n) 
    { 
        // If number becomes N-digit, print it 
        if (n == 0) 
        { 
            System.out.print(out + " "); 
            return; 
        } 
   
        // start from (prev digit + 1) till 9 
        for (int i = start; i <= 9; i++) 
        { 
            // append current digit to number 
            String str = out + Integer.toString(i); 
   
            // recurse for next digit 
            findStrictlyIncreasingNum(i + 1, str, n - 1); 
        } 
    } 
  
    // Driver code for above function 
    public static void main(String args[])throws IOException 
    { 
        Increasing obj = new Increasing(); 
        int n = 3; 
        obj.findStrictlyIncreasingNum(0, " ", n); 
    }  
} 
```
## Print sums of all subsets of a given set
```java
import java .io.*; 
  
class GFG  
{ 
      
    // Prints sums of all  
    // subsets of arr[l..r] 
    static void subsetSums(int []arr, int l, 
                            int r, int sum ) 
    { 
          
        // Print current subset 
        if (l > r) 
        { 
            System.out.print(sum + " "); 
            return; 
        } 
      
        // Subset including arr[l] 
        subsetSums(arr, l + 1, r,  
                   sum + arr[l]); 
      
        // Subset excluding arr[l] 
        subsetSums(arr, l + 1, r, sum); 
    } 
      
    // Driver code 
    public static void main (String[] args) 
    { 
        int []arr = {5, 4, 3}; 
        int n = arr.length; 
      
        subsetSums(arr, 0, n - 1, 0); 
    } 
} 
```
## Find ways an Integer can be expressed as sum of n-th power of unique natural numbers
```java
class GFG 
{ 
      
// Function to calculate and return the  
// power of any given number  
static int power(int num, int n)  
{  
    if (n == 0)  
        return 1;  
    else if (n % 2 == 0)  
        return power(num, n / 2) * power(num, n / 2);  
    else
        return num * power(num, n / 2) * power(num, n / 2);  
}  
  
// Function to check power representations recursively  
static int checkRecursive(int x, int n, int curr_num,int curr_sum)  
{  
    // Initialize number of ways to express  
    // x as n-th powers of different natural  
    // numbers  
    int results = 0;  
  
    // Calling power of 'i' raised to 'n'  
    int p = power(curr_num, n);  
    while (p + curr_sum < x)  
    {  
        // Recursively check all greater values of i  
        results += checkRecursive(x, n, curr_num + 1,  
                                        p + curr_sum);  
        curr_num++;  
        p = power(curr_num, n);  
    }  
  
    // If sum of powers is equal to x  
    // then increase the value of result.  
    if (p + curr_sum == x)  
        results++;  
  
    // Return the final result  
    return results;  
}  
  
// Driver Code. 
public static void main (String[] args)  
{ 
    int x = 10, n = 2;  
    System.out.println(checkRecursive(x, n, 1, 0)); 
}  
}
```
## Recaman’s sequence
```java
import java.io.*; 
  
class GFG { 
      
    // Prints first n terms of Recaman sequence 
    static void recaman(int n) 
    { 
        // Create an array to store terms 
        int arr[] = new int[n]; 
      
        // First term of the sequence is always 0 
        arr[0] = 0; 
        System.out.print(arr[0]+" ,"); 
      
        // Fill remaining terms using recursive 
        // formula. 
        for (int i = 1; i < n; i++) 
        { 
            int curr = arr[i - 1] - i; 
            int j; 
            for (j = 0; j < i; j++) 
            { 
                // If arr[i-1] - i is negative or 
                // already exists. 
                if ((arr[j] == curr) || curr < 0) 
                { 
                    curr = arr[i - 1] + i; 
                    break; 
                } 
            } 
      
            arr[i] = curr; 
            System.out.print(arr[i]+", "); 
              
        } 
    } 
      
    // Driver code 
    public static void main (String[] args)  
    { 
        int n = 17; 
        recaman(n); 
  
    } 
}
```
## Program for Sum of the digits of a given number
```java
import java.io.*; 
  
class GFG { 
      
    /* Function to get sum of digits */
    static int getSum(int n) 
    {     
        int sum = 0; 
          
        while (n != 0) 
        { 
            sum = sum + n % 10; 
            n = n/10; 
        } 
      
    return sum; 
    } 
  
    // Driver program 
    public static void main(String[] args) 
    { 
        int n = 687; 
  
        System.out.println(getSum(n)); 
    } 
} 
```
## Count ways to express a number as sum of powers
```java
public class GFG {  
  
    // num is current num. 
    static int countWaysUtil(int x, int n, int num) 
    { 
        // Base cases 
        int val = (int) (x - Math.pow(num, n)); 
        if (val == 0) 
            return 1; 
        if (val < 0) 
            return 0; 
       
        // Consider two possibilities, num is 
        // included and num is not included. 
        return countWaysUtil(val, n, num + 1) + 
               countWaysUtil(x, n, num + 1); 
    } 
       
    // Returns number of ways to express 
    // x as sum of n-th power of two. 
    static int countWays(int x, int n) 
    { 
        return countWaysUtil(x, n, 1); 
    } 
       
    // Driver code 
    public static void main(String args[]) 
    { 
        int x = 100, n = 2; 
        System.out.println(countWays(x, n)); 
    } 
}
```
## Find m-th summation of first n natural numbers.
```java
class GFG { 
      
    // Function to return mth summation 
    static int SUM(int n, int m) { 
          
        // base case 
        if (m == 1) 
            return (n * (n + 1) / 2); 
      
        int sum = SUM(n, m - 1); 
          
        return (sum * (sum + 1) / 2); 
    } 
      
    // Driver code 
    public static void main(String[] args) { 
          
        int n = 5; 
        int m = 3; 
          
        System.out.println("SUM(" + n + ", "
                        + m + "): "    + SUM(n, m)); 
    } 
} 
```
## Generate all passwords from given character set
``` java
import java.util.*; 
  
class GFG 
{ 
  
    // int cnt; 
    // Recursive helper function, adds/removes characters 
    // until len is reached 
    static void generate(char[] arr, int i, String s, int len) 
    { 
        // base case 
        if (i == 0) // when len has been reached 
        { 
            // print it out 
            System.out.println(s); 
              
            // cnt++; 
            return; 
        } 
  
        // iterate through the array 
        for (int j = 0; j < len; j++) 
        { 
  
            // Create new string with next character 
            // Call generate again until string has 
            // reached its len 
            String appended = s + arr[j]; 
            generate(arr, i - 1, appended, len); 
        } 
  
        return; 
    } 
  
    // function to generate all possible passwords 
    static void crack(char[] arr, int len) 
    { 
        // call for all required lengths 
        for (int i = 1; i <= len; i++) 
        { 
            generate(arr, i, "", len); 
        } 
    } 
  
    // Driver code 
    public static void main(String[] args) 
    { 
        char arr[] = {'a', 'b', 'c'}; 
        int len = arr.length; 
        crack(arr, len); 
    } 
  
}
```
## Print N-bit binary numbers having more 1’s than 0’s in all prefixes
```java
import java.io.*;
 
class GFG {
    // function to generate n digit numbers
    static void printRec(String number, 
                         int extraOnes,
                         int remainingPlaces)
    {
        // if number generated
        if (0 == remainingPlaces) {
            System.out.print(number + " ");
            return;
        }
 
        // Append 1 at the current number and
        // reduce the remaining places by one
        printRec(number + "1", extraOnes + 1,
                 remainingPlaces - 1);
 
        // If more ones than zeros, append 0 to the
        // current number and reduce the remaining
        // places by one
        if (0 < extraOnes)
            printRec(number + "0", extraOnes - 1,
                     remainingPlaces - 1);
    }
 
    static void printNums(int n)
    {
        String str = "";
        printRec(str, 0, n);
    }
 
    // Driver code
    public static void main(String[] args)
    {
        int n = 4;
       
        // Function call
        printNums(n);
    }
}
```
## Minimum tiles of sizes in powers of two to cover whole area
```java
class GFG { 
      
    static int minTiles(int n, int m) 
    { 
    // base case, when area is 0. 
    if (n == 0 || m == 0) 
        return 0; 
      
    // If n and m both are even,  
    // calculate tiles for n/2 x m/2 
    // Halving both dimensions doesn't  
    // change the number of tiles 
    else if (n % 2  == 0 && m % 2 == 0) 
        return minTiles(n / 2, m / 2); 
          
    // If n is even and m is odd 
    // Use a row of 1x1 tiles 
    else if (n % 2 == 0 && m % 2 == 1) 
        return (n + minTiles(n / 2, m / 2)); 
      
    // If n is odd and m is even 
    // Use a column of 1x1 tiles 
    else if (n % 2 == 1 && m % 2 == 0) 
        return (m + minTiles(n / 2, m / 2)); 
      
    // If n and m are odd 
    // add row + column number of tiles 
    else
        return (n + m - 1 + minTiles(n / 2, m / 2));  
    } 
          
    // Driver code 
    public static void main (String[] args) 
    { 
            int n = 5, m = 6; 
            System.out.println(minTiles(n, m)); 
    } 
}
```
## Alexander Bogomolny’s UnOrdered Permutation Algorithm
```java
import java.io.*; 
  
class GFG 
{ 
static int level = -1; 
  
// A function to print 
// the permutation. 
static void print(int perm[], int N) 
{ 
    for (int i = 0; i < N; i++) 
        System.out.print(" " + perm[i]); 
    System.out.println(); 
} 
  
// A function implementing  
// Alexander Bogomolyn algorithm. 
static void AlexanderBogomolyn(int perm[],  
                               int N, int k) 
{ 
  
    // Assign level to  
    // zero at start. 
    level = level + 1; 
    perm[k] = level; 
  
    if (level == N) 
        print(perm, N); 
    else
        for (int i = 0; i < N; i++) 
  
            // Assign values  
            // to the array  
            // if it is zero. 
            if (perm[i] == 0) 
                AlexanderBogomolyn(perm, N, i); 
  
    // Decrement the level  
    // after all possible  
    // permutation after  
    // that level. 
    level = level - 1; 
      
    perm[k] = 0; 
} 
  
// Driver Code 
public static void main (String[] args) 
{ 
    int i, N = 3; 
    int perm[] = new int[N]; 
    AlexanderBogomolyn(perm, N, 0); 
} 
} 
```
## Sum of natural numbers using recursion
```java
import java.util.*; 
import java.lang.*; 
  
class GFG 
{ 
  
    // Returns sum of first  
    // n natural numbers 
    public static int recurSum(int n) 
    { 
        if (n <= 1) 
            return n; 
        return n + recurSum(n - 1); 
    } 
      
    // Driver code 
    public static void main(String args[]) 
    { 
        int n = 5; 
        System.out.println(recurSum(n)); 
    } 
} 
```
## Decimal to binary number using recursion
```java
import java.io.*; 
  
class GFG  
{ 
      
    // Decimal to binary conversion  
    // using recursion 
    static int find(int decimal_number) 
    { 
        if (decimal_number == 0)  
            return 0;  
              
        else
          
        return (decimal_number % 2 + 10 *  
                find(decimal_number / 2)); 
    } 
      
// Driver Code 
public static void main(String args[]) 
{ 
    int decimal_number = 10; 
    System.out.println(find(decimal_number)); 
} 
  
}
```
## Sum of digit of a number using recursion
```java
import java.io.*; 
  
class sum_of_digits 
{ 
    // Function to check sum  
    // of digit using recursion 
    static int sum_of_digit(int n) 
    {  
        if (n == 0) 
            return 0; 
        return (n % 10 + sum_of_digit(n / 10)); 
    } 
  
    // Driven Program to check above 
    public static void main(String args[]) 
    { 
        int num = 12345; 
        int result = sum_of_digit(num); 
        System.out.println("Sum of digits in " +  
                           num + " is " + result); 
    } 
}
```
## Binary to Gray code using recursion
```java
import static java.lang.StrictMath.pow; 
import java.util.Scanner; 
  
class bin_gray 
{ 
    // Function to change Binary to 
    // Gray using recursion 
    int binary_to_gray(int n, int i) 
    {  
        int a, b; 
        int result = 0; 
        if (n != 0)  
        { 
            // Taking last digit 
            a = n % 10;  
              
            n = n / 10; 
              
            // Taking second last digit 
            b = n % 10;  
          
            if ((a & ~ b) == 1 || (~ a & b) == 1)  
            { 
                result = (int) (result + pow(10,i)); 
            } 
              
            return binary_to_gray(n, ++i) + result; 
        } 
        return 0; 
    } 
  
    // Driver Function 
    public static void main(String[] args) 
    { 
        int binary_number; 
        int result = 0; 
        binary_number = 1011101; 
          
        bin_gray obj = new bin_gray(); 
        result = obj.binary_to_gray(binary_number,0); 
          
        System.out.print(result); 
    }  
}
```
## Number of non-negative integral solutions of sum equation
```java
class GFG { 
  
  // return number of non negative 
  // integral solutions 
  static int countSolutions(int n, int val) { 
  
    // initialize total = 0 
    int total = 0; 
  
    // Base Case if n = 1 and val >= 0 
    // then it should return 1 
    if (n == 1 && val >= 0) 
      return 1; 
  
    // iterate the loop till equal the val 
    for (int i = 0; i <= val; i++) { 
  
      // total solution of equations 
      // and again call the recursive 
      // function Solutions(variable, value) 
      total += countSolutions(n - 1, val - i); 
    } 
  
    // return the total no possible solution 
    return total; 
  } 
  
  // Driver code 
  public static void main(String[] args) { 
    int n = 5; 
    int val = 20; 
  
    System.out.print(countSolutions(n, val)); 
  } 
} 
```
## Product of 2 Numbers using Recursion
```java
import java.io.*; 
import java.util.*; 
  
class GFG  
{ 
      
    // recursive function to calculate  
    // multiplication of two numbers 
    static int product(int x, int y) 
    { 
        // if x is less than  
        // y swap the numbers 
        if (x < y) 
            return product(y, x); 
      
        // iteratively calculate  
        // y times sum of x 
        else if (y != 0) 
            return (x + product(x, y - 1)); 
      
        // if any of the two numbers is  
        // zero return zero 
        else
            return 0; 
    } 
      
    // Driver Code 
    public static void main (String[] args) 
    { 
        int x = 5, y = 2; 
        System.out.println(product(x, y));  
    } 
}
```
## Recursive program for prime number
```java
import java.util.*; 
  
class GFG { 
  
    // Returns true if n is prime, else 
    // return false. 
    // i is current divisor to check. 
    static boolean isPrime(int n, int i) 
    { 
  
        // Base cases 
        if (n <= 2) 
            return (n == 2) ? true : false; 
        if (n % i == 0) 
            return false; 
        if (i * i > n) 
            return true; 
       
        // Check for next divisor 
        return isPrime(n, i + 1); 
    } 
      
    // Driver program to test above function  
    public static void main(String[] args) 
    { 
  
        int n = 15; 
  
        if (isPrime(n, 2))  
            System.out.println("Yes"); 
        else 
            System.out.println("No"); 
    } 
} 
```
## Print all combinations of factors (Ways to factorize)
```java
import java.io.*; 
import java.util.*; 
class FactorsCombination { 
  
    // Returns a list containing all ways to factorize 
    // a number n. 
    public static List<List<Integer> > factComb(int n) 
    { 
        // making list of lists to store all 
        // possible combinations of factors 
        List<List<Integer> > result_list = 
                     new ArrayList<List<Integer> >(); 
        List<Integer> list = new ArrayList<Integer>(); 
  
        // function to calculate all the combinations 
        // of factors 
        factorsListFunc(2, 1, n, result_list, list); 
        return result_list; 
    } 
  
    // First is current factor to be considered. 
    // each_product is current product of factors.     
    public static void factorsListFunc(int first,  
                             int each_prod, int n,  
    List<List<Integer> > result_list, List<Integer>         
                               single_result_list) 
    { 
        // Terminating condition of this recursive  
        // function 
        if (first > n || each_prod > n) 
            return; 
  
        // When each_prod is equal to n, we get 
        // the list of factors in 'single_result_ 
        // _list' so it is  added to the result_ 
        // _list list . 
        if (each_prod == n) { 
  
            ArrayList<Integer> t = 
          new ArrayList<Integer>(single_result_list); 
  
            result_list.add(t); 
  
            return; 
        } 
  
        // In this loop we first calculate factors 
        // of n and then it's combination so that 
        // we get the value n in a recursive way . 
        for (int i = first; i < n; i++) { 
            if (i * each_prod > n) 
                break; 
  
            // if i divides n 
            // properly then it 
            // is factor of n 
            if (n % i == 0) { 
  
                // it is added to 'single_result_list' list 
                single_result_list.add(i); 
  
                // Here function is called recursively 
                // and when (i*each_prod) is equal to n 
                // we will store the 'single_result_list' (it is 
                // basically the list containing all 
                // combination of factors) into result_list. 
                factorsListFunc(i, i * each_prod, n, 
                  result_list, single_result_list); 
  
                // here we will empty the 'single_result_list'  
                // List so that new combination of factors 
                // get stored in it. 
                single_result_list.remove(single_result_list.size() - 1); 
            } 
        } 
    } 
  
    // Driver code 
    public static void main(String[] args) 
    { 
        int n = 16; 
        List<List<Integer> > resultant = factComb(n); 
  
        // printing all possible combination 
        // of factors stored in resultant list 
        for (List<Integer> i : resultant) { 
            for (int j : i)  
                System.out.print(j + " ");             
            System.out.println(); 
        } 
    } 
} 
```