## Permutation

```java
import java.util.ArrayList;

public class Permutation {
    private String in;
    private ArrayList<String> a = new ArrayList<String>();
    // additional attribute if needed
    public int start;


    Permutation(final String str){
        in = str;
        // additional initialization if needed
        start = 0;

    }

    public void permute(){
        // produce the permuted sequence of 'in' and store in 'a', recursively
        int end = in.length() -1;

        if (start == end){
            a.add(in);
        }
        else{
            for (int i=start; i<= end; i++){
                in = permuting(in, start, i);
                start +=1;
                permute();
                start -=1;
                in = permuting(in, start, i);
                if (a.contains(in)){
                    continue;
                }
                a.add(in);
            }
        }
    }

    private String permuting(String in, int start, int i) {
        char placeHolder;
        char[] inArray = in.toCharArray();
        placeHolder = inArray[start];
        inArray[start] = inArray[i];
        inArray[i] = placeHolder;
        return String.valueOf(inArray);
    }

    public ArrayList<String> getA(){
        return a;
    }
}

class TestPermutation {
    public static void main(String[] args) {
        ArrayList<String> v;

        Permutation p = new Permutation("hat");
        p.permute();
        v = p.getA();
        System.out.println(v);

    }
}
```

## GetPath
```java
import java.util.ArrayList;

public class GetPath {
    public ArrayList<Point> getPath(final int[][] grid){
        if(grid != null || grid.length != 0){
            ArrayList<Point> paths = new ArrayList<>();
            if (getPath(0,0, paths, grid)){
                return paths;
            }
        }
        return null;
    }


    //Fill in your answer for this method
    public static boolean getPath (int r, int c, ArrayList<Point> path, final int [][] grid) {
        if (r == 0 && c == 0){
            return true;
        }
        if (r > grid.length || c > grid[0].length){
            return false;
        }

        if (r < 0 || c < 0 || grid[r][c] == 1){
            return false;
        }
        if (grid[0][1] == 1 && grid[1][0] == 1 && grid[1][1] == 1){
            return false;
        }
        if (grid[r][c-1] == 1 && grid[r-1][c] == 1 && grid[r-1][c-1] == 1){
            return false;
        }
        if (getPath(r, c-1, path, grid) || getPath(r-1, c, path, grid)){
            Point p = new Point(r, c);
            path.add(p);
            return true;
        }
        return false;

    }
}

//You do not need to change any code below ---------
class Point {
    int x;
    int y;

    Point (int x, int y) {
        this.x=x;
        this.y=y;
    }

    public String toString() {
        return "(" + x + "," + y + ")";
    }
}
//--------------------------------------------------

class TestRobot {

    public static void main(String[] args) {

        final int[][] grid = {
                {0,0,0,1},
                {0,1,0,0},
                {0,1,1,1},
                {0,0,0,1},
                {1,1,1,1},
                {1,1,1,0}
        };


        ArrayList<Point> path = new ArrayList<>();

        boolean success = GetPath.getPath(5, 3, path, grid);

        System.out.println(success);
        if (success)
            System.out.println(path);
        path.clear();


    }


}
```
## AirPollution Alert
```java
interface Observer{
    void update(double airPollutionIndex);
}

class Subscriber implements Observer{
    private Subject subject;
    private String observerId;
    public static String outputMessage = "";

    public Subscriber(String observerId, Subject subject){
        this.subject=subject;
        this.observerId = observerId;
        this.subject.register(this);		// register itself
    }

    @Override
    public void update(double airPollutionIndex) {
        String s = this.observerId + " received notification: " + airPollutionIndex;
        System.out.println(s);
        outputMessage += (s + " ");
    }
}

interface Subject{
    void register(Observer o);
    void unregister(Observer o);
    void notifyObservers();
}
//-------------------------------------------------------

//TODO: modify AirPollutionAlert to implement interface Subject, under Observer design pattern
class AirPollutionAlert implements Subject{
    private double airPollutionIndex;

    public void setAirPollutionIndex(double airPollutionIndex) {
        this.airPollutionIndex = airPollutionIndex;
        if (this.airPollutionIndex > 100){
            notifyObservers();
        }
    }

    private java.util.ArrayList<Observer> observerList = new java.util.ArrayList<Observer>();

    @Override
    public void register(Observer o) {
        observerList.add(o);

    }

    @Override
    public void unregister(Observer o) {
        observerList.remove(o);
    }

    @Override
    public void notifyObservers() {
        for (Observer o : observerList) {
            o.update(airPollutionIndex);
        }
    }
}
```
## Instance Implementation
```java
public class TestClass {

    //DO NOT MODIFY THIS METHOD
    public static void main(String[] args) {
        C2 x = new C2();

        System.out.println(x instanceof I1);
        System.out.println(x instanceof I2);
        System.out.println(x instanceof I3);
        System.out.println(x instanceof I4);
        System.out.println(x instanceof I5);
        System.out.println(x instanceof C1);

        C3 y = new C3();

        System.out.println(y instanceof I1);
        System.out.println(y instanceof I2);
        System.out.println(y instanceof I3);
        System.out.println(y instanceof I4);
        System.out.println(y instanceof I5);

    }
}

// Modify from here onwards ....
// Add and modify the code for interfaces and classes according to the question

interface I1{
    int p1();
}
interface I2{
    int p2();
}
interface I3{
    int p3();
}
interface I4 extends I1, I2, I3{
    int p4();
}
interface I5 extends I3{
    int p5();
}

class C3 implements I5 {

    @Override
    public int p5() {
        return 0;
    }

    @Override
    public int p3() {
        return 0;
    }
}
abstract class C1 implements I4 {
    abstract int q1();
}

class C2 extends C1 implements I5 {

    @Override
    public int p1() {
        return 0;
    }

    @Override
    public int p4() {
        return 0;
    }

    @Override
    public int p2() {
        return 0;
    }

    @Override
    public int p3() {
        return 0;
    }

    @Override
    int q1() {
        return 0;
    }

    @Override
    public int p5() {
        return 0;
    }
}
```

## Exception Handling
```java
public class TestException {
    //YOU DO NOT NEED TO MODIFY THIS METHOD
    public static void main(String[] args) {
        String[] in = {"hello", "good night", "good morning"};

        String ret = tstException(2, in);

        System.out.println(ret);

        ret = tstException(-1, in);

        System.out.println(ret);
    }

    //IMPLEMENT YOUR SOLUTION IN THIS METHOD
    public static String tstException(int idx, String[] y) {
        // implement using try-catch
        try{
            return y[idx];
        }catch (Exception e){
            return "Out of Bounds";
        }

    }
}
```
## Palindrome
```java
import java.util.Arrays;

public class Palindrome {
    public static boolean isPalindrome (char[] S) {
        if (S.length == 0 | S.length == 1){
            return true;
        }
        else if (S[0] == S[S.length-1]){
            StringBuilder S_array = new StringBuilder(String.valueOf(S));
            S_array.deleteCharAt(0);
            S_array.deleteCharAt(S.length-2);
            return isPalindrome(S_array.toString().toCharArray());
        }
        else{
            return false;
        }

    }

    public static String Palindrome(String inp){
        if (isPalindrome(inp.toCharArray())){
            return inp + " is a palindrome.";
        }else{
            return inp + " is not a palindrome.";
        }
    }


}
```
## Comparator
```java
import java.util.Comparator;

public class Octagon{
    private double side;
    public Octagon(double side){
        this.side = side;
    }
    public double getSide() {
        return side;
    }

}

public class OctagonComparator implements Comparator<Octagon> {

    @Override
    public int compare(Octagon o1, Octagon o2) {
        return Double.compare(o1.getSide(), o2.getSide());
    }
}
```
## Test Temperature
```java
import java.sql.SQLOutput;
import java.util.ArrayList;

public class TestTemperatureAlert {
    public static void main(String[] args) {
        TemperatureAlert westCoast = new TemperatureAlert();
        Student s1 = new Student("s1", westCoast);
        Student s2 = new Student("s2", westCoast);
        westCoast.setTemperature(40);
        westCoast.setTemperature(25);
        westCoast.setTemperature(5);
        westCoast.unregister(s1);
        Student s3 = new Student("s3", westCoast);
        Fish f1 = new Fish("f1", westCoast);
        westCoast.setTemperature(2);
    }
}

interface Subject{
    void register(Observer o);
    void unregister(Observer o);
    void notifyObservers();
}

interface Observer{
    void update(int temp);
}

class TemperatureAlert implements Subject{
    private int temp;
    private ArrayList<Observer> observers;

    TemperatureAlert() {
        this.observers = new ArrayList<>();
    }

    @Override
    public void register(Observer o) {
        observers.add(o);
    }

    @Override
    public void unregister(Observer o) {
        observers.remove(o);
    }

    @Override
    public void notifyObservers() {
        if (this.temp > 35 || this.temp < 10) {
            for (Observer o : observers) {
                o.update(this.temp);
            }
        }
    }

    public void setTemperature(int i){
        this.temp= i;

        notifyObservers();

    }
}

class Student implements Observer{
    private int temp;
    private Subject subject;
    private String id;

    public Student(String id, Subject subject){
        this.id = id;
        this.subject = subject;
        this.subject.register(this);
    }

    @Override
    public void update(int temp) {
        this.temp = temp;

        System.out.println("Student" + this.id + "receives temperature alert:" + this.temp);
    }
}

class Fish implements Observer{
    private int temp;
    private Subject subject;
    private String id;

    public Fish(String id, Subject subject){
        this.id = id;
        this.subject = subject;
        this.subject.register(this);
    }

    @Override
    public void update(int temp) {
        this.temp = temp;

        System.out.println("Fish" + this.id + "receives temperature alert:" +this.temp);
    }

}
```
## Fibbonacci
```java
import java.util.ArrayList;

public class Fib {

    public static ArrayList<Integer> a = new ArrayList<>();

    public static void main(String[] args) {
        System.out.println(recurFib(3));
        System.out.println(recurFib(5));
        System.out.println(recurFib(10));
    }
    public static int recurFib(int idx) {
        //TODO: implement recursive method
        System.out.println(a.toString());

        if (idx == 0){
            int out = a.get(a.size() -1);
            a.clear();
            return out;
        }

        else{
            if(a.size() != 2){
                a.add(1);
            }
            else if (a.size() == 2){
//                System.out.println(a.get(0) + a.get(1));
                a.add(a.get(0) + a.get(1));
                a.remove(0);
            }
            return recurFib(idx-1);
        }

    }

}
```
## Print all possible strings of length k that can be formed from a set of n characters
```java
import java.util.ArrayList;
import java.util.Arrays;
import java.util.List;

public class AllSeq {
    public static void main(String[] args) {
        String[] s = {"p", "q"};
        System.out.println(compAllSeq(s, 3));
        String[] s2 = {"1", "2", "3", "4"};
        System.out.println(compAllSeq(s2, 1));
    }
    public static ArrayList<String> compAllSeq(String[] s, int k){
        //TODO: implement a recursive method to return all possible sequences of length k
        if(k == 1){
            return new ArrayList<>(Arrays.asList(s));
        }
        else{
            ArrayList<String> result = new ArrayList<String>();
            for(String i:compAllSeq(s, k-1)){
                for (String j :s){
                    result.add(j+i);
                }
            }
            return result;
        }
    }

}
```
## Strongly Connected Graph
```java
import java.util.ArrayList;
import java.util.Arrays;

public class StronglyConnected {
    static boolean testStronglyConnected(int nodecount, int linkcount, ArrayList<Integer> listOfLink)
    { //TODO


        for (int i = 0; i< nodecount; i++){
            for (int j = 0; j< nodecount; j++){
//                System.out.println(String.valueOf(i) + String.valueOf(j));
                if(!findPath(i, j, linkcount, listOfLink)){
                    return false;
                }

            }
        }
//        System.out.println("here 2");
        return true;
    }

        public static boolean findPath(int start, int end, int linkcount, ArrayList<Integer> listOfLink){
            if(start == end){
//                System.out.println("here 3");
                return true;
            }

            for (int i = 0; i < linkcount * 2; i+=2){
                if(listOfLink.get(i) == start){
                    if (listOfLink.get(i+1) == end){
                        return true;
                    }
                    else{
                        return findPath(listOfLink.get(i+1), end, linkcount, listOfLink);
                    }
                }
            }
            return false;
        }
    }



class TestStronglyConnected	{
    public static void main	(String[]	args){
        int nodecount=4;
        int linkcount=4;
        ArrayList<Integer>	listOfLink	=	new ArrayList<Integer>	(	Arrays.asList(0,1,		1,2,		2,3 ,  3,0));
        System.out.println(StronglyConnected.testStronglyConnected(nodecount,	linkcount,	listOfLink));
    }
}
```
## Account
```java
import java.util.ArrayList;
import java.util.Collections;
import java.util.Comparator;
import java.util.Date;

public class Account implements Comparable<Account>{
    private String id;
    private double balance;
    private Date dateCreated;

    public Account(String id, double balance) {
        this.id = id;
        this.balance = balance;
    }

    public String getId() {
        return id;
    }

    public double getBalance() {
        return balance;
    }

    public Date getDateCreated() {
        return dateCreated;
    }

    @Override
    public String toString() {
        String s = "Account:" + this.id;
        return s;
    }

    public int compareTo(Account a){
        return (int) (this.balance - a.balance);
    }

}

class AccountComparator implements Comparator<Account>{
    @Override
    public int compare(Account account, Account t1) {
        String id1 = account.getId();
        String id2 = t1.getId();

        if (id1.charAt(0) < id2.charAt(0)){
            return -1;
        }
        else if (id1.charAt(0) == id2.charAt(0)){
            return 0;
        }
        else{
            return 1;
        }
    }
}

class TestAcc {
    public static void main(String[] args) {
        Account a = new Account("simon", 20);
        System.out.println(a.getId());
        System.out.println(a.getBalance());
        System.out.println(a);
        ArrayList<Account> l = new ArrayList<>();
        l.add(new Account("man", 30));
        l.add(new Account("eric", 100));
        l.add(new Account("norman", 10));
        Collections.sort(l);
        System.out.println(l);
        Collections.sort(l, new AccountComparator());
        System.out.println(l);
    } }
```


 