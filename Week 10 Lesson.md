# Week 10 Lesson

#### Abstract Classes and Abstract Methods
To use an abstract class, sub-class it and implement any abstract methods.

```java=
public abstract class CaffeineBeverage{
    boilWater();
    brew();
    addCondiments();
    pourInCup();
}
    
    abstract void brew();
    
    abstract void addCondiments();
    
    void boilWater(){
        System.out.println("Boiling Water");
    }
    
    void pourInCup(){
        System.out.println("Pouring in cup");
    }
```
In sub-class
```java=
class GourmetCoffee extends CaffeineBeverage{
    @Override
    void brew(){
        System.out.println("Put in coffee maker");
    }
    
    @Override
    void addCondiments(){
        System.out.println("Adding nothing, because GourmetCoffee");
    }
}
```
```java=
CaffeineBeverage caffeineBeverage = new GourmetCoffee();
caffeineBeverage.prepareRecipe();
```
#### AsyncTasks Abstract class
Allows us to run tasks in the background, "asynchronously".

```java=
// AsyncTask<Params, Progress, Result>

class MyBackgroundTask extens AsyncTask<URL, Void, Bitmap>{
    
    @Override
    protected Bitmap doInBackground(URL... urls){
        Bitmap bitmap = null;
        return bitmap;
    }
    
    @Override
    protected void onProgressUpdate(String... values){
        super.onProgressUpdate(values);
    }
    
    @Override
    protected void onPostExecute(Bitmap bitmap){
        super.onPostExecute(bitmap);
    }
}
```
In `setOnClickListener()`,
```java=
GetComic getComic = new GetComic();
getComic.execute(url);
```
#### Building a URL
```java
final String scheme = "https";
final String authority = "xkcd.com";
final String back = "info.0.json";

URL url = null;

Uri.Builder builder = new Uri.Builder();
builder.scheme(scheme)
       .authority(authority)
       .appendPath(back);

Uri uri = builder.build();

try{
    url = new URL(uri.toString());
}catch (MalformedURLException ex){
    Log.i(TAG, "malformed URL: " + url.toString());
}
```

In android manifest, to allow for access to internet:
```java=
<uses-permission android:name="android.permission.INTERNET" />

<uses-permission android:name="android.permission.ACCESS_NETWORK_STATE" />
```