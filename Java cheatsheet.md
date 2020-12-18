# Java cheatsheet

1. Primitive Data Types

|Type     |Size |
| ----------- | ----------- |
| byte    | 8       |
| short   | 16        |
| int    | 32       |
| long   | 64        |
| float    | 32       |
| double   | 32        |
| char    | 16       |
| Boolean   | 1        |

2. Java operators

|Type     |Operatora |
| ----------- | ----------- |
| Arithmetic    | "+", "-", "*", "%", "//", "/"       |
| Assignment   | "=", "+=", "-=", "*=", "/=", "&=", "^=" |
| Bitwise    | "^", "&", "I"       |
| Logical   | "&&", "II"        |
| Relational    | "<", ">", "<=", ">=", "==",  "!="  |

3. Iterative Statements

```java
// for loop
for (condition) {
	expression
}

// for each loop
for (int i : someArray){}

//for iterator loop
for (int i = 0; i<10; i++){}

//while loop
while (condition) {
	expression
}

//do while loop
do {expression} while(condition)
```

4. Arrays in Java
```java
//List

int intArray[] = new int["Size of array"];
byte byteArray[] = new byte["Size of array"];
short shortsArray[] = new short["Size of array"];
boolean booleanArray[] = new boolean["Size of array"];
long longArray[] = new long["Size of array"];
float floatArray[] = new float["Size of array"];
double doubleArray[] = new double["Size of array"];
char charArray[] = new char["Size of array"];
String[] strArray = new String["Size of array"]


//changing item in array
String[] cars = {"Volvo", "BMW", "Ford", "Mazda"};
cars[0] = "Opel";

//finding array length
String[] cars = {"Volvo", "BMW", "Ford", "Mazda"};
System.out.println(cars.length);

//looping through the array
String[] cars = {"Volvo", "BMW", "Ford", "Mazda"};
for (int i = 0; i < cars.length; i++) {
  System.out.println(cars[i]);
}
//or
for (String i : cars) {
  System.out.println(i);
}

-----------------------------------------------------------------------------
//ArrayList
List<Integer> arrayList = new ArrayList<>();

//changing item in array
arrayList.add(13);
arrayList.set(index: 4, int: 3);
arrayList.get(index: 5);

arrayList.remove(index: 5);
arrayList.remove(int: 13);
arrayList.removeAll(arrayList2)
arrayList.clear();

//finding array length
arrayList.size();

//looping through the array
while (arrayList.hasNext()) {
	Integer element = arrayList.next();
	System.out.println(element);
}

for(Integer element: arrayList){
	System.out.println(element);
}

for(int i = 0; i < arrayList.size(); i++) {
	System.out.println(String(valueOf.(arrayList.get(i))));
}
```

5. String Methods

|Method	|Description	|Return Type|
| ----------- | ----------- |----------- |
|charAt()	|Returns the character at the specified index (position)	|char|
|compareTo()	|Compares two strings lexicographically	|int|
|contains()	|Checks whether a string contains a sequence of characters|	boolean|
|endsWith()	|Checks whether a string ends with the specified character(s)|	boolean|
|equals()	|Compares two strings. Returns true if the strings are equal, and false if not	|boolean|
|indexOf()	|Returns the position of the first found occurrence of specified characters in a string	|int|
|length()	|Returns the length of a specified string	|int|
|replace()	|Searches a string for a specified value, and returns a new string where the specified values are replaced	|String|
|replaceFirst()	|Replaces the first occurrence of a substring that matches the given regular expression with the given replacement	|String|
|replaceAll()	|Replaces each substring of this string that matches the given regular expression with the given replacement	|String|
|split()	|Splits a string into an array of substrings	|String[]|
|startsWith()	|Checks whether a string starts with specified characters	|boolean|
|substring()	|Extracts the characters from a string, beginning at a specified start position, and through the specified number of character	|String|
|toCharArray()	|Converts this string to a new character array	|char[]|

6. Math Method

|Method	|Description	|Return Type|
| ----------- | ----------- |----------- |
|abs(x)	|Returns the absolute value of x	|double I float I int I long|
|exp(x)	|Returns the value of Ex	|double|
|max(x, y)	|Returns the number with the highest value	|double I float I int I long|
|min(x, y)	|Returns the number with the lowest value	|double I float I int I long|
|random()	|Returns a random number between 0 and 1	|double|
|sqrt(x)	|Returns the square root of x	|double|

7. Conversion methods

**String -> Integer**
Method 1
```java
public static void main(String args[]){
	String str="123";
	int inum = 100;

	int inum2 = Integer.parseInt(str); //inum2 = int 123
		
	int sum = inum+inum2;
	System.out.println("Result is: "+sum);
   }
```
```java
out = 223
```
Method 2
```java
String str="-1122";
int inum = Integer.valueOf(str); // inum = int -1122
```

**String -> char[]**
```java
public static void main(String[] args) {
		String testString = "This Is Test";
		char[] stringToCharArray = testString.toCharArray();
		}
	}
```
8. HashMap Method
![[Pasted image 20201209124549.png]]
