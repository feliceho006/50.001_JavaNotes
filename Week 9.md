# Week 9

#### BigDecimal class
```java=
System.out.println(0.7 + 0.1);
```
> Console: 0.799999999

In a computer, decimal value is represented into 2 parts.
1. Integer value
2. c represents the scale
- i x b^c, b is the base which can be 10, 2
> 1 x 10^-2 = 0.25

#### Exceptions 
Put a code in a `try-catch` block.
`ArithmeticException` is:
- subclass of `RuntimeException`, such exceptions are thrown by JVM <font size="2">(The JVM manages system memory and provides a portable execution environment for Java-based applications. The Java Virtual Machine is a program whose purpose is to execute other programs)</font> 
- unchecked exception, you do not need to implement the code in `try-catch` during compile (`NumberFormatException` is another example)

```java=
public class ExceptionsExample{
    public static void main(String[] args){
        try{
            int a = quotientInt(5,0);
        }catch(ArithmeticException aex){
            aex.printStackTrace();
        }
    }
    
    public static int quotientInt(int a, int b){
        return a/b;
    }
}
```

#### Static Factory Method
A static method in a class definition that returns an instance of the class. *\not factory design pattern

When overloading your constructor to initialise a class with different stats, you are constrained to having the same name for all constructors.

```java=
//Without static factory method
public class Tea{
    private boolean sugar;
    private boolean milk;
    
    Tea(boolean sugar, boolean milk){
        this.sugar = sugar;
        this.milk = milk;
    }
    
    Tea(){
    }
    
    Tea(boolean sugar){
        this.sugar = sugar;
    }

}
```
```java=
//With static factory method
public class Tea{
    private boolean sugar;
    private boolean milk;
    
    Tea(boolean sugar, boolean milk){
        this.sugar = sugar;
        this.milk = milk;
    }
    
    public static Tea teh(){
        return new Tea(true, true);
    }
    
    public static Tea tehkosong(){
        return new Tea(false, true);
    }
}

//invoke static factor method like this
Tea tea = Tea.tehkohsong();
```

#### Toasts
1. call the static factory method `makeText()`
    - Context Object (`super-class` of `AppCompatActivity`), ie which activity will the toast be seen
    - String
    - Duration of toast (`Toast.LENGTH_SHORT` or `Toast.LENGTH_LONG`)
```java=
Toast.makeText(MainActivity.this, R.string.warning, Toast.LENGTH_SHORT).show();
```

#### Logcat
Logcat messages type: `d` for debug, `w` for warning, `e` for error, `i` for info

```java=
Log.i(TAG, "String here");
```
`TAG` is a String variable that is `final` and `static`.

#### Explicit Intent vs Implicit Intent
> Explicit Intent

Use explicit intent when you know exactly which Activity can handle your request.

Example: You have a `List Activity` and when you click an item in the list it opens a `Detail activity`. In this case, you KNOW that the details of the item can be shown or handled by `DetailActivity.class` of your application. So to perform this action you create an Intent by explicitly specifying the class name.

```java=
Intent intent = new Intent(this,DetailActivy.class);  
startActivity(intent);
```

**To pass data**
```java=
Intent intent = new Intent(MainActivity.this, SubActivity.class);
intent.putExtra(KEY, value);
startActivity(intent);
```
In SubActivity
```java=
Intent intent = getIntent();
double value = intent.getDoubleExtra(MainActivity.KEY, defaultValue);
```
> Implicit Intent

Use implicit intent when you don't know which activity of which application/s can handle your request.

Example: You have a link. When you click the link it should open the webpage in some browser. You DON'T KNOW exactly which `Activity` in which application can handle your request. You just have a vague idea that its a webpage link so it should open a webpage in some browser when someone opens it. In this case, you just specify the `ACTION` and then OS takes care of the rest.

```java=
Intent intent = new Intent(Intent.ACTION_VIEW, Uri.parse(url));
startActivity(intent);
```
#### Android Activity Lifecycle

![](https://i.imgur.com/TQhpJwX.png)

**Data persistence with Shared Preferences**
1. declare filename of `SharedPreferences` object as a final string instance variable
2. declare a key as final string instance variable
3. In `onCreate()`, get instance of `SharedPreferences` object
4. In `onPause()`, get instance of `SharedPreferences.Editor` object and store key-value pairs.
5. In `onCreate()`, retrieve data using key, and assign default value. 

```java=

private final String sharedPrefFile = "filename"
private static final String KEY = "KEY_VALUE"
SharedPreferences mPreferences;

@Override
protected void onCreate(Bundle savedInstanceState){
    //other codes
    mPreferences = getSharedPreferences(sharedPrefFile, MODE_PRIVATE);
    String Rate_text = mPreferences.getString(KEY, defaultValue);
}

@Override
protected void onPause () {
    super .onPause();
    SharedPreferences.Editor preferencesEditor =
            mPreferences.edit();
    preferencesEditor.putString(KEY, value);
    preferencesEditor.apply();
}
```

#### Builder Design Pattern
```java=
public class TeaTwo{
    private boolean sugar;
    private boolean milk;
    private boolean ice;
    private boolean toGo;
    
    //private constructor    
    private TeaTwo(TeaBuilder teaBuilder){
        this.sugar = teaBuilder.sugar;
        this.milk = teaBuilder.milk;
        this.ice = teaBuilder.ice;
        this.toGo = teaBuilder.toGo;
    }
    
    static class TeaBuilder{
        private boolean sugar;
        private boolean milk;
        private boolean ice;
        private boolean toGo;
    }
    
    TeaBuilder(){
    }
    
    public Teabuilder setSugar(boolean sugar){
        this.sugar = sugar;
        return this;
    }
    
    : // repeat for all variables
    .
    
    public Teabuilder setToGo(boolean toGo){
        this.toGo = toGo;
        return this;
    }
    
    
    public TeaTwo build(){
        return new TeaTwo(this);
    }
}
```
```java=
TeaTwo teaTwo() = new TeaTwo.setsugar(true)
                            .setMilk(true).build()
```

#### Unit Testing
Ensure that each of the components behave as designed.
```java=
@Test
public void addition_isCorrect(){
    assetEquals(expected, actual);
}

//for example
@Test(expected= IllegalArguementException.class)
public void someFunction(){
    new A(). someFunction("apple");
}
```